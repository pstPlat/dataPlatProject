<template>
<div class="modal-container">
  <!--默认链接邀请 000-->
  <div class="modal-item" v-if="dataflag==='000'">
     <div class="item-body">
        <div class="item-title">
          <p>通过微信扫码，邀请成员</p>
          <img src="https://p.ssl.qhimg.com/d/inn/0444533a/Snip20160525_6.png" alt="" >
        </div>
       <div>
          <p class="action"><span @click="toEmail" >邮箱邀请</span><span @click="toPhone">手机号邀请</span></p>
       </div>
     </div>
    <div class="item-footer">
      <p>通过发送链接，邀请成员</p>
       <div> <a-input style="margin-right:5px;width:290px;" v-model="urlInfo"></a-input> <a-button type="primary" @click="copyUrl(urlInfo)">复制链接</a-button></div>
    </div>
  </div>
  <!--邮箱邀请 001-->
  <!--手机号邀请002-->
  <div class="modal-item" v-else>
    <div class="item-body">
      <div class="item-title" v-if="dataflag==='001'">
        <p>通过邮箱邀请项目组成员</p>
        <p >今日可邀请次数{{mobilelimitNumber}}</p>
      </div>
      <div class="item-title" v-else>
        <p>通过手机号邀请项目组成员</p>
        <p >今日可邀请次数{{emailLimitNum}}</p>
      </div>
      <div>
        <p class="action" v-if="dataflag==='001'"><span @click="toPhone" >手机号邀请</span><span @click="toUrl">链接邀请</span></p>
        <p class="action" v-else><span @click="toEmail" >邮箱邀请</span><span @click="toUrl">链接邀请</span></p>
      </div>
    </div>
    <div class="item-info" >
      <add-info  ref="mobileInfo" :dataflag="dataflag" :key="dataflag"></add-info>
    </div>

    <div class="item-info">
      <a-button type="primary"  @click="sendCode(dataflag)">发送邀请</a-button>
    </div>
  </div>
</div>
</template>

<script>
  import AddInfo from './addInfo'
    export default {
        name: "modalInfo",
      components:{AddInfo},
      data(){
          return{
            dataflag:'000',
            urlInfo:'www.baidu.com',
            mobilelimitNumber:10,
            emailLimitNum:9,
            phoneArr:[]
          }
      },
      methods:{
          copyUrl(data){
            let url = data;
            let oInput = document.createElement('input');
            oInput.value = url;
            document.body.appendChild(oInput);
            oInput.select(); // 选择对象;
            oInput.style.display='none'
            document.execCommand("Copy"); // 执行浏览器复制命令
            this.$message.success('复制成功,点击粘贴');
          },
        toEmail(){
             this.dataflag='001'
        },
        toPhone(){
          this.dataflag='002'
        },
        toUrl(){
            this.dataflag='000'
        },
        sendCode(key){
          this.$refs.mobileInfo.handleSubmit();

          }
      },
      beforeCreate(){
        this.form = this.$form.createForm(this);
        this.form.getFieldDecorator('keys', { initialValue: [], preserve: true });
      }
    }
</script>

<style scoped>
 .modal-container{

 }
 .item-title{
   color: rgba(0, 0, 0, 0.65);
   line-height:22px;
   text-align:center;
 }
 .item-title img{
   width:112px;
   height:112px;

 }
  .item-body{
       display:flex;
      justify-content: space-between;
  }
  .action{
    text-align:left;
  }
  .action span{
    cursor:pointer;
    text-decoration: underline;
    font-size: 14px;
    line-height: 22px;
    letter-spacing: 0px;
    color: #1890ff;
    text-align:left;
  }
  .action span:nth-child(2){
    margin-left:24px;
  }
 .item-footer .ant-input{
   width: 200px;
   margin-right:5px;
 }
 .item-footer div{
   display:flex;
 }
  .item-title p:nth-of-type(2){
    color: rgba(0, 0, 0, 0.25);
  }
 .item-info{
   margin-top:40px;
 }
</style>

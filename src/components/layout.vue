<template>
	<div id="layout">
		<div class="app-head">
			<div class="app-head-inner">
				<div class="head-logo">
					<img src="../assets/logo.png"/>	
				</div>
				<div class="head-nav">
					<ul class="nav-list">
						<li v-if="!!userName" v-html="userName"></li>
						<li v-if="!!userName" class="nav-pile">|</li>
						<li v-if="!!userName" @click="outClick">退出</li>
						<li v-if="!!userName" class="nav-pile">|</li>
						<li v-if="!userName" @click="logClick">登录</li>
						<li v-if="!userName" class="nav-pile">|</li>
						<li v-if="!userName" @click="regClick">注册</li>
						<li v-if="!userName" class="nav-pile">|</li>
						<li @click="abortClick">关于</li>
					</ul>
				</div>
			</div>
		</div>
		<div class="app-content">
			<keep-alive>
				<router-view></router-view>
			</keep-alive>
		</div>
		<div class="app-foot">
			<p>© 2016 fishenal MIT</p>
		</div>
		<my-dialog :is-show="isShowLogDialog" @on-close="closeDialog('isShowLogDialog')" >
			<log-from @has-log = "onSucessLogin"></log-from>
		</my-dialog>
		<my-dialog :is-show="isShowRegDialog" @on-close="closeDialog('isShowRegDialog')">
			<p>reg hello</p>
		</my-dialog>
		<my-dialog :is-show="isShowAboutDialog" @on-close="closeDialog('isShowAboutDialog')">
			<p>本报告在调研数据的基础上，采用定性与定量相结合的方式深入分析了专车市场发展的驱动因素与阻碍因素、专车市场背后的产业格局、专车企业的竞争格局、用户对专车市场的依赖程度、专车对其他交通工具运力的补充效应等，通过这五个章节的研究反映专车市场的发展态势和面临的问题。报告力求客观、深入、准确地反映中国专车市场发展情况，为政府、企事业单位和社会各界提供决策依据。 </p>
		</my-dialog>
		
	</div>
</template>

<script>
	import Dialog from './dialog'
	import LogFrom from './logFrom'
	export default {
		components :{
			MyDialog: Dialog,
			LogFrom
		},
		data () {
			return {
				isShowLogDialog:false,
				isShowRegDialog:false,
				isShowAboutDialog:false,
				userName:null,
			}
		},
		methods : {
			logClick () {
				this.isShowLogDialog = true;
			},
			regClick () {
				this.isShowRegDialog = true;
			},
			abortClick () {
				this.isShowAboutDialog = true;
			},
			closeDialog (attr) {
				this[attr] = false; 
			},
			onSucessLogin(data){
				this.userName = data.name;
				this.closeDialog('isShowLogDialog')
			},
			outClick () {
				this.userName = null;
				this.isShowLogDialog = false;
				this.isShowRegDialog = false;
				this.isShowAboutDialog = false;
			}
		}
	}
</script>

<style>
	
html, body, div, span, applet, object, iframe,
h1, h2, h3, h4, h5, h6, p, blockquote, pre,
a, abbr, acronym, address, big, cite, code,
del, dfn, em, img, ins, kbd, q, s, samp,
small, strike, strong, sub, sup, tt, var,
b, u, i, center,
dl, dt, dd, ol, ul, li,
fieldset, form, label, legend,
table, caption, tbody, tfoot, thead, tr, th, td,
article, aside, canvas, details, embed, 
figure, figcaption, footer, header, hgroup, 
menu, nav, output, ruby, section, summary,
time, mark, audio, video {
  margin: 0;
  padding: 0;
  border: 0;
  font-size: 100%;
  font: inherit;
  vertical-align: baseline;
}
/* HTML5 display-role reset for older browsers */
article, aside, details, figcaption, figure, 
footer, header, hgroup, menu, nav, section {
  display: block;
}
body {
  line-height: 1;
}
ol, ul {
  list-style: none;
}
blockquote, q {
  quotes: none;
}
blockquote:before, blockquote:after,
q:before, q:after {
  content: '';
  content: none;
}
table {
  border-collapse: collapse;
  border-spacing: 0;
}
a {
  color: inherit;
  text-decoration: none;
}
body {
  background: #f0f2f5;
  font-family: "Helvetica Neue",Helvetica,Arial,"Hiragino Sans GB","Hiragino Sans GB W3","Microsoft YaHei UI","Microsoft YaHei","WenQuanYi Micro Hei",sans-serif;
  font-size: 14px;
  color: #444;
}

.button {
  background: #4fc08d;
  color: #fff;
  display: inline-block;
  padding: 10px 20px;
  cursor: pointer;
}
.button:hover {
  background: #4fc08d;
}
.app-head {
  background: #363636;
  color: #b2b2b2;
  height: 90px;
  line-height: 90px;
  width: 100%;
}
.app-head-inner {
  width: 1200px;
  margin: 0 auto;
}
.head-logo {
  float: left;
}
.app-head-inner img {
  width: 50px;
  margin-top: 20px;
}
.head-nav {
  float: right;
}
.head-nav ul {
  overflow: hidden;
}
.head-nav li {
  cursor: pointer;
  float: left;
}
.nav-pile {
  padding: 0 10px;
}
.app-content{
	width: 1000px;
    margin: 0 auto;
}
.app-foot {
  text-align: center;
  height: 80px;
  width: 100%;
  line-height: 80px;
  background: #e3e4e8;
  clear: both;
  margin-top: 30px;
}


.g-form {

}
.g-form-line {
  padding: 15px 0;
}
.g-form-label {
  width: 100px;
  font-size: 16px;
  display: inline-block;
}
.g-form-input {
  display: inline-block;
}
.g-form-input input {
  height: 30px;
  width: 200px;
  line-height: 30px;
  vertical-align: middle;
  padding: 0 10px;
  border: 1px solid #ccc;
}
.g-form-btn {
  padding-left: 100px;
}
.g-form-error {
  color: red;
  padding-left: 15px;
}
</style>
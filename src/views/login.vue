 <template>
	<div id="login">
		<ul class="formUl">
			<li>账号</li>
			<li><input type="text" placeholder="手机号码" /></li>
			<li>密码</li>
			<li><input type="password" placeholder="输入密码" /></li>
			<li><a>登录</a></li>
			<li><i></i><router-link to="/register">注册账号</router-link></li>
		</ul>
	</div>
</template>
<script type="es6">
  import { PLAY_AUDIO } from '../mixins'
  export default {
    mixins: [PLAY_AUDIO],
    data(){
      return {
        opacity: 0
      }
    },
    //通过路由的before钩子解除router-view缓存限制
    beforeRouteEnter (to, from, next) {
      next(vm => {
        vm.$store.commit('showHead', true);
        vm.get();
        window.onscroll = ()=> {
          vm.opacity = window.pageYOffset / 250;
          vm.$store.commit('setHeadStyle', {background: `rgba(43,162,251,${vm.opacity})`});
        }
      })
    },
    beforeRouteLeave(to, from, next){
      this.$store.commit('showHead', false);
      window.onscroll = null;
      next();
    }
  }
</script>
<style lang="scss" scoped>
    @import "../assets/core/reset.scss"; 
    #login {
        @include flexbox();
        @include flex-direction(column);
        width: 100%;
        height: 100%;
        .back {
            @include flexbox();
            width: 100%;
            height: .44rem;
            line-height: .44rem;
            border-bottom: 1px solid #ddd;
            background: #33CCCC;
            color: #fff;
            padding-right: .1rem;
            .iconfont {
                width: .5rem;
                font-size: 20px;
                font-weight: bolder;
                text-align: center;
            }
            a {
                width: .5rem;
                color: #fff;
                text-align: center;
                font-size: 12px;
            }
            i {
                @include flex();
                font-size: 15px;
               
            }
        }
        .formUl {
            @include flex();
            width: 100%;
            padding-top: .3rem;
            li {
                width: 100%;
                text-align: center;
                padding: 5px;
                input {
                    width: 100%;
                    font-size: 20px;
                    border: none;
                    border-bottom: 1px solid #C4C4C4;     
                    text-align: center;                                 
                }  
                input::-webkit-input-placeholder { 
                    color: #ccc; 
                }
                &:nth-child(5) {
                    margin-top: .2rem;
                    a {
                        display: inline-block;
                        width: 100%;
                        padding: 6px 0;
                        background: #33CCCC;
                        color: #fff;
                        font-size: 16px;
                        border-radius: 8px;
                        
                    }      
                } 
                &:nth-child(6) {
                    width: 100%;
                    @include flexbox();
                    @include justify-content(space-between);
                    i {
                        @include flex();
                    }
                    a {
                        font-size: 12px;           
                        &:last-child {
                            color: #33CCCC;
                        }
                    }
                  
                }
               
            }
            
        }
    }
</style>


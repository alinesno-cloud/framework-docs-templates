<template>
  <div class="home">
    <div class="hero">

      <h1>{{ title }}</h1>

      <p class="description">
        AlinesnoCloud 是一款高性能、轻量级的开源 Java 服务框架
      </p>

      <p v-if="data.actionText && data.actionLink" class="action">
        <NavLink class="action-button" :item="actionLink" />
      </p>
    </div>

    <div class="features-box">
      <div v-if="featuresAll.length" class="features">
          <div v-for="(feature, index) in featuresAll" :key="index" class="feature">
            <div class="title-icon"><i :class="feature.icon"></i></div>
            <h3>{{ feature.title }}</h3>
            <p>{{ feature.details }}</p>
          </div>
      </div>
    </div>

    <div class="hero-section">
      <p class="title"> 谁在使用 Dubbo </p>
      <p class="description">
        请在 XXXX 上提供信息来帮助 Dubbo 做的更好
      </p>
    </div>

    <div class="footer-section">
        <ul>
          <li>
            <p class="icon"><i class="fas fa-envelope"></i></p>
            <p class="label">订阅邮件组</p>
            <p class="tip">luoandong@gmail.com</p>
          </li>
          <li>
            <p class="icon"><i class="fab fa-github"></i></p>
            <p class="label">欢迎参与贡献！</p>
            <p class="tip">在 GitHub 上协作。我们期待您的加入！</p>
          </li>
          <li>
            <p class="icon"><i class="fab fa-weixin"></i></p>
            <p class="label">请关注我们的公众号！</p>
            <p class="tip">我们会在第一时间分享新发布的特性和使用心得</p>
          </li>
        </ul>
    </div>

    <Content custom />

    <div v-if="data.footer" class="footer">{{ data.footer }}</div>
  </div>
</template>

<script>
import NavLink from '@default-theme/NavLink.vue'
import { isGitee } from './utils'

export default {
  components: { NavLink },
  data() {
    return {
      title: '服务化引擎框架',
      featuresAll: [
        {
          title: '面向接口代理的高性能RPC调用',
          details:
            '提供高性能的基于代理的远程调用能力，服务以接口为粒度，为开发者屏蔽远程调用底层细节。',
          icon: 'fas fa-space-shuttle'
        },
        {
          title: '智能负载均衡',
          details:
            '内置多种负载均衡策略，智能感知下游节点健康状况，显著减少调用延迟，提高系统吞吐量。',
          icon: 'fab fa-angular'
        },
        {
          title: '服务自动注册与发现',
          details: '支持多种注册中心服务，服务实例上下线实时感知。',
          icon: 'fas fa-charging-station'
        },
        {
          title: '高度可扩展能力',
          details:
            '遵循微内核+插件的设计原则，所有核心能力如Protocol、Transport、Serialization被设计为扩展点，平等对待内置实现和第三方实现。',
          icon: 'fas fa-chalkboard'
        },
        {
          title: '运行期流量调度',
          details:
            '内置条件、脚本等路由策略，通过配置不同的路由规则，轻松实现灰度发布，同机房优先等功能。',
          icon: 'fas fa-code'
        },
        {
          title: '可视化的服务治理与运维',
          details:
            '提供丰富服务治理、运维工具：随时查询服务元数据、服务健康状态及调用统计，实时下发路由策略、调整配置参数。',
          icon: 'fab fa-angular'
        }
      ]
    }
  },
  computed: {
    isCN() {
      // return this.$lang === 'zh-CN'
      return true
    },
    isGitee() {
      if (this.$isServer) return
      return isGitee()
    },
    data() {
      return this.$page.frontmatter
    },
    actionLink() {
      return {
        link: this.data.actionLink,
        text: this.data.actionText
      }
    }
  },
  methods: {
    clickCoding(tag) {
      ga('send', 'click', 'e.coding', 'Action', tag)
    }
  }
}
</script>

<style lang="stylus">
 @import '~@default-theme/styles/config.styl';

$accentColor = #005bd4

.home {
  padding: $navbarHeight 0rem 0;
  max-width: 100%;
  margin: 0px auto;

  .hero {
    text-align: center;
    padding: 4.5rem 0px;

    >img {
      max-height: 280px;
      display: block;
      margin: 3rem auto 1.5rem;
    }

    h1 {
      font-size: 2rem;
    }

    h1, .description, .action {
      margin: 1.8rem auto;
    }

    .description {
      max-width: 35rem;
      font-size: 1.25rem ;
      line-height: 1.3;
      color: lighten($textColor, 40%);
    }

    .action-button {
      display: inline-block;
      font-size: 1.2rem;
      color: #fff;
      background-color: $accentColor;
      padding: 0.8rem 1.6rem;
      border-radius: 4px;
      transition: background-color 0.1s ease;
      box-sizing: border-box;
      border-bottom: 1px solid darken($accentColor, 10%);

      &:hover {
        background-color: lighten($accentColor, 10%);
      }
    }
  }

  .features-box{
    background-color : #f7fbfd ;
    padding: 10px 0px;
  }

  .features {
    padding: 1.2rem 0;
    margin-top: 2.5rem;
    display: flex;
    flex-wrap: wrap;
    align-items: flex-start;
    align-content: stretch;
    justify-content: space-between;
    text-align: center ;
    background-color : #f7fbfd ;
    max-width: 1560px;
    margin: auto;
  }

  .feature {
    flex-grow: 1;
    flex-basis: 30%;
    max-width: 30%;

    h2 {
      font-size: 1.4rem;
      font-weight: 500;
      border-bottom: none;
      padding-bottom: 0;
      color: lighten($textColor, 10%);
    }

    p {
      color: lighten($textColor, 25%);
    }
  }

  .footer {
    padding: 2.5rem;
    text-align: center;
    color: lighten($textColor, 25%);
  }
}

.footer-section {
    text-align: center;
    padding: 4rem 0px;
    background-color: #403f4c;
    float:left  ; 
    width: 100% ;
    margin-bottom: 50px;

    p{
      color: #fff ;
      line-height: .9rem;
    }

    ul{
        float :left ;
        max-width: 1560px ; 
        width : 100%;
        margin: auto ;
    }

    li{
      float: left ;
      width: 33% ;
    }

    .icon{
      font-size: 1.8rem;
      line-height: 0.5rem;
      padding: 0px;
      margin: 10px;
    }
}


.hero-section {
    text-align: center;
    padding: 1.8rem 0px;

   .title{
     font-size: 1.2rem;
   }

    .description {
      font-size: 1.25rem ;
      line-height: 1.3;
      color: #333 ; 
    }
}

@media (max-width: $MQMobile) {
  .home {
    .features {
      flex-direction: column;
    }

    .feature {
      max-width: 100%;
      padding: 0 2.5rem;
    }
  }
}

@media (max-width: $MQMobileNarrow) {
  .home {
    padding-left: 1.5rem;
    padding-right: 1.5rem;

    .hero {
      img {
        max-height: 210px;
        margin: 2rem auto 1.2rem;
      }

      h1 {
        font-size: 2rem;
      }

      h1, .description, .action {
        margin: 1.2rem auto;
      }

      .description {
        font-size: 1.2rem;
      }

      .action-button {
        font-size: 1rem;
        padding: 0.6rem 1.2rem;
      }
    }

    .feature {
      h2 {
        font-size: 1.25rem;
      }
    }
  }
}

.title-icon{
  font-size:2.2rem ;
  color: $accentColor;
}

</style>

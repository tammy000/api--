<style scoped>
  .headerWrapper {
    height: 50px;
  }

  .header {
    height: 50px;
    top: 0;
    left: 0;
    width: 100%;
    position: relative;
    background: #111;
    background-image: linear-gradient(bottom, #005199 20%, #0069aa 80%);
    background-image: -o-linear-gradient(bottom, #005199 20%, #0069aa 80%);
    background-image: -moz-linear-gradient(bottom, #005199 20%, #0069aa 80%);
    background-image: -webkit-linear-gradient(bottom, #005199 20%, #0069aa 80%);
    background-image: -ms-linear-gradient(bottom, #005199 20%, #0069aa 80%);
    background-image: -webkit-gradient( linear, left bottom, left top, color-stop(0.2, #005199), color-stop(0.8, #0069aa) );
    padding: 10px 0;
    color: #fafafa;
    border-bottom: solid 1px #004893;
    box-shadow: 0 0 20px 0px #034282;
    position: fixed;
    z-index: 100;
    line-height: @height;

    .container {
      height: 100%;
      box-sizing: border-box;
    }

    .nav-lang-spe {
      color: #888;
    }

    h1 {
      margin: 0;
      float: left;
      font-size: 32px;
      font-weight: normal;

      a {
        color: #333;
        text-decoration: none;
        display: block;
      }

      span {
        font-size: 12px;
        display: inline-block;
        width: 34px;
        height: 18px;
        border: 1px solid rgba(255, 255, 255, .5);
        text-align: center;
        line-height: 18px;
        vertical-align: middle;
        margin-left: 10px;
        border-radius: 3px;
      }
    }

    .nav {
      float: right;
      height: 100%;
      line-height: 50px;
      background: transparent;
      @utils-clearfix;
      padding: 0;
      margin: 0;
    }

    .nav-gap {
      position: relative;
      width: 1px;
      height: 50px;
      padding: 0 20px;

      &::before {
        content: '';
        position: absolute;
        top: calc(50% - 8px);
        width: 1px;
        height: 16px;
        background: #ebebeb;
      }
    }

    .nav-logo,
    .nav-logo-small {
      vertical-align: sub;
    }

    .nav-logo-small {
      display: none;
    }

    .nav-item {
      margin: 0;
      float: left;
      list-style: none;
      position: relative;
      cursor: pointer;
    
      &.nav-algolia-search {
        cursor: default;
      }
    
      &.lang-item,
      &:last-child {
        cursor: default;
        margin-left: 34px;

        span {
          opacity: .8;
        }

        .nav-lang {
          cursor: pointer;
          display: inline-block;
          height: 100%;
          color: #ffffff;

          &:hover {
            color: #409EFF;
          }
          &.active {
             font-weight: bold;
             color: #409EFF;
           }
        }
      }

      a {
        text-decoration: none;
        color: #ffffff;
        display: block;
        padding: 0 22px;

        &.active,
        &:hover {
          color: #409EFF;
        }

        &.active::after {
          content: '';
          display: inline-block;
          position: absolute;
          bottom: -11px;
          left: calc(50% - 10px);
          width: 20px;
          height: 4px;
          background: #409EFF;
        }
      }
    }
  }

  .nav-dropdown {
    margin-bottom: 6px;
    padding-left: 18px;
    width: 100%;

    span {
      display: block;
      width: 100%;
      font-size: 16px;
      color: #ffffff;
      line-height: 40px;
      transition: .2s;
      padding-bottom: 6px;
      user-select: none;

      &:hover {
         cursor: pointer;
       }
    }

    i {
      transition: .2s;
      font-size: 12px;
      color: #979797;
      transform: translateY(-2px);
    }

    @when active {
      span, i {
        color: #409EFF;
      }
      i {
        transform: rotateZ(180deg) translateY(3px);
      }
    }

    &:hover {
      span, i {
        color: #409EFF;
      }
    }
  }
  
  .nav-dropdown-list {
    width: auto;
  }

  @media (max-width: 850px) {
    .header {
      .nav-logo {
        display: none;
      }
      .nav-logo-small {
        display: inline-block;
      }
      .nav-item {
        margin-left: 6px;

        &.lang-item,
        &:last-child {
          margin-left: 10px;
        }
         
        a {
          padding: 0 5px;
        }
      }
      .nav-theme-switch, .nav-algolia-search {
        display: none;
      }
    }
  }

  @media (max-width: 700px) {
    .header {
      .container {
        padding: 0 12px;
      }
      .nav-item {
        a {
          font-size: 12px;
          vertical-align: top;
        }

        &.lang-item {
          height: 100%;
         
          .nav-lang {
            display: flex;
            align-items: center;
            
            span {
              padding-bottom: 0;
            }
          }
        }
      }
      .nav-dropdown {
        padding: 0;
        span {
          font-size: 12px;
        }
      }
      .nav-gap {
        padding: 0 8px;
      }
    }
  }
</style>
<template>
  <div class="headerWrapper">
    <header class="header" ref="header">
      <div class="container">
        <h1><router-link :to="`/${ lang }`">
          <!-- logo -->
          <font style="vertical-align: inherit;color:#fff;">MTIGIS</font>

        </router-link></h1>

        <!-- nav -->
        <ul class="nav">
          <li class="nav-item nav-algolia-search" v-show="isComponentPage">
            <algolia-search></algolia-search>
          </li>
          <li class="nav-item">
            <router-link
              active-class="active"
              :to="`/${ lang }/guide`">{{ langConfig.guide }}
            </router-link>
          </li>
          <li class="nav-item">
            <router-link
              active-class="active"
              :to="`/${ lang }/component`">{{ langConfig.components }}
            </router-link>
          </li>
          <li class="nav-item">
            <router-link
              active-class="active"
              :to="`/${ lang }/resource`"
              exact>{{ langConfig.resource }}
            </router-link>
          </li>

          <!-- gap -->
          <li class="nav-item" v-show="isComponentPage">
            <div class="nav-gap"></div>
          </li>

          <!-- 语言选择器 -->
          <li class="nav-item lang-item">
            <el-dropdown
              trigger="click"
              class="nav-dropdown nav-lang"
              :class="{ 'is-active': langDropdownVisible }">
              <span>
                {{ displayedLang }}
                <i class="el-icon-arrow-down el-icon--right"></i>
              </span>
              <el-dropdown-menu
                slot="dropdown"
                class="nav-dropdown-list"
                @input="handleLangDropdownToggle">
                <el-dropdown-item
                  v-for="(value, key) in langs"
                  :key="key"
                  @click.native="switchLang(key)">
                  {{ value }}
                </el-dropdown-item>
              </el-dropdown-menu>
            </el-dropdown>
          </li>
          
          <!--theme picker-->
          <!-- <li class="nav-item nav-theme-switch" v-show="isComponentPage">
            <theme-picker></theme-picker>
          </li> -->
        </ul>
      </div>
    </header>
  </div>
</template>
<script>
  import ThemePicker from './theme-picker.vue';
  import AlgoliaSearch from './search.vue';
  import compoLang from '../i18n/component.json';
  import Element from 'main/index.js';

  export default {
    data() {
      return {
        active: '',
        verDropdownVisible: true,
        langDropdownVisible: true,
        langs: {
          'zh-CN': '中文',
          'en-US': 'English'
        }
      };
    },

    components: {
      ThemePicker,
      AlgoliaSearch
    },

    computed: {
      lang() {
        return this.$route.path.split('/')[1] || 'zh-CN';
      },
      displayedLang() {
        return this.langs[this.lang] || '中文';
      },
      langConfig() {
        return compoLang.filter(config => config.lang === this.lang)[0]['header'];
      },
      isComponentPage() {
        return /^component/.test(this.$route.name);
      }
    },

    methods: {
      switchLang(targetLang) {
        if (this.lang === targetLang) return;
        localStorage.setItem('ELEMENT_LANGUAGE', targetLang);
        this.$router.push(this.$route.path.replace(this.lang, targetLang));
      },

      handleVerDropdownToggle(visible) {
        this.verDropdownVisible = visible;
      },

      handleLangDropdownToggle(visible) {
        this.langDropdownVisible = visible;
      }
    },

    created() {
      
    }
  };
</script>

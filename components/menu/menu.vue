<template>
  <div>
    <!-- button -->
    <button class="btn toggle_btn" @click="showMenu = !showMenu">
      <fa icon="bars" ></fa>
    </button>

    <!-- menu view -->
    <div v-if="showMenu" class="sidbar_main_wrap">
      <a
      href="#"
      @click="showMenu = !showMenu"
      class="close_sidebar"
        ><fa icon="times"></fa
      ></a>
      <div class="sidebar_menu">
        <div class="sidebar_menu_inner">
          <ul>
            <!-- category -->
            <li
              class="sidebar_item"
              v-for="category in tempData"
              :key="category.uid"
            >
              <a href="#">
                {{ category.name }}

                <div v-if="category.children.length" @click="showOrHideList(category)">
                  <fa
                    icon="chevron-right"
                    v-if="!category.showSub"
                  ></fa>
                  <fa
                    icon="chevron-down"
                    v-if="category.showSub"
                  ></fa>
                </div>
              </a>
              <!-- sub category -->
              <ul
                class="sidebar_submenu"
                v-if="category.children.length && category.showSub"
              >
                <li
                  class="sidebar_item sidebar_submenu_item"
                  v-for="subCategory in category.children"
                  :key="subCategory.uid"
                >
                  <a href="#">
                    {{ subCategory.name }}
                    <div v-if="subCategory.children.length" @click="showOrHideList(subCategory)">
                      <fa
                    icon="chevron-right"
                    v-if="!subCategory.showSub"
                  ></fa>
                  <fa
                    icon="chevron-down"
                    v-if="subCategory.showSub"
                  ></fa>
                    </div>
                  </a>

                  <!-- sub category item -->
                  <ul
                    class="sidebar_submenu"
                    v-if="subCategory.children.length && subCategory.showSub"
                  >
                    <li
                      class="sidebar_item"
                      v-for="subCatItem in subCategory.children"
                      :key="subCatItem.uid"
                    >
                      <a href="#">{{ subCatItem.name }}</a>
                    </li>
                  </ul>
                </li>
              </ul>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data () {
    return {
      showMenu: false,
      tempData: [
        {
          // showSub: false,
          children_count: '38',
          uid: 'Mg==',
          level: 1,
          name: 'Default Category',
          path: '1/2',
          url_path: null,
          url_key: null,
          children: [
            {
              uid: 'MjA=',
              level: 2,
              name: 'Women',
              path: '1/2/20',
              url_path: 'women',
              url_key: 'women',
              children: [
                {
                  uid: 'MjE=',
                  level: 3,
                  name: 'Tops',
                  path: '1/2/20/21',
                  url_path: 'women/tops-women',
                  url_key: 'tops-women'
                },
                {
                  uid: 'MjI=',
                  level: 3,
                  name: 'Bottoms',
                  path: '1/2/20/22',
                  url_path: 'women/bottoms-women',
                  url_key: 'bottoms-women'
                }
              ]
            },
            {
              uid: 'OQ==',
              level: 2,
              name: 'Training',
              path: '1/2/9',
              url_path: 'training',
              url_key: 'training',
              children: [
                {
                  uid: 'MTA=',
                  level: 3,
                  name: 'Video Download',
                  path: '1/2/9/10',
                  url_path: 'training/training-video',
                  url_key: 'training-video'
                }
              ]
            },
            {
              uid: 'MTE=',
              level: 2,
              name: 'Men',
              path: '1/2/11',
              url_path: 'men',
              url_key: 'men',
              children: [
                {
                  uid: 'MTI=',
                  level: 3,
                  name: 'Tops',
                  path: '1/2/11/12',
                  url_path: 'men/tops-men',
                  url_key: 'tops-men'
                },
                {
                  uid: 'MTM=',
                  level: 3,
                  name: 'Bottoms',
                  path: '1/2/11/13',
                  url_path: 'men/bottoms-men',
                  url_key: 'bottoms-men'
                }
              ]
            },
            {
              uid: 'Mw==',
              level: 2,
              name: 'Gear',
              path: '1/2/3',
              url_path: 'gear',
              url_key: 'gear',
              children: [
                {
                  uid: 'NA==',
                  level: 3,
                  name: 'Bags',
                  path: '1/2/3/4',
                  url_path: 'gear/bags',
                  url_key: 'bags'
                },
                {
                  uid: 'NQ==',
                  level: 3,
                  name: 'Fitness Equipment',
                  path: '1/2/3/5',
                  url_path: 'gear/fitness-equipment',
                  url_key: 'fitness-equipment'
                },
                {
                  uid: 'Ng==',
                  level: 3,
                  name: 'Watches',
                  path: '1/2/3/6',
                  url_path: 'gear/watches',
                  url_key: 'watches'
                }
              ]
            },
            {
              uid: 'Mzg=',
              level: 2,
              name: "What's New",
              path: '1/2/38',
              url_path: 'what-is-new',
              url_key: 'what-is-new',
              children: []
            },
            {
              uid: 'Mzc=',
              level: 2,
              name: 'Sale',
              path: '1/2/37',
              url_path: 'sale',
              url_key: 'sale',
              children: []
            }
          ]
        }
      ]
    }
  },
  created () {
    this.getMenuData()
  },

  methods: {
    showOrHideList (catData) {
      console.log(catData, this.tempData[0])
      if (catData.showSub) {
        catData.showSub = !catData.showSub
      } else {
        catData.showSub = true
      }
      console.log(catData)
      console.log(this.tempData)
      this.$forceUpdate()
    },

    getMenuData () {
      const data = JSON.stringify({
        query: `
       query categoryList(
          filters: {

          }
        ) {
          children_count
          uid
            level
            name
            path
            url_path
            url_key
          children {
            uid
            level
            name
            path
            url_path
            url_key
            children {
              uid
              level
              name
              path
              url_path
              url_key
            }
          }
        }
      `,
        variables: {}
      })

      // const data = JSON.stringify({
      //   query: `
      // query PostsForAuthor {
      //   author(id: 1) {
      //     firstName
      //       posts {
      //         title
      //         votes
      //       }
      //     }
      //   }
      // `
      // })

      const config = {
        method: 'post',
        url: 'https://m2.antarctica.test.e-bricks.cloud/graphql',
        // url: 'https://1jzxrj179.lp.gql.zone/graphql',
        headers: {
          'Content-Type': 'application/json'
          // Cookie: 'PHPSESSID=jr92crdckkr3a7rvk2t2vmpjva; private_content_version=305cf5fad0ce2f441e4ac8ca0df78238'
        },
        data
      }

      axios(config)
        .then((response) => {
          console.log(response.data)
        })
        .catch((error) => {
          console.log(error)
        })
    }
  }
}
</script>

<style scoped>
@import url("./style.css");
</style>

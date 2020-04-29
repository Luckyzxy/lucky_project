<template>
  <div style="overflow: hidden;">
    <van-sidebar style="width: 25%; float: left;" v-model="activeKey">
      <van-sidebar-item v-for="i in list" :key="i" :title=i.name @click="mym(i.id)" />
    </van-sidebar>
    <div style="width: 75%; float: left;" class="w">
      <van-grid :border="false">
        <van-grid-item v-for="i in arr" :key="i" :icon="i.bz_1" :text="i.name" @click="xq(i.id)" />
      </van-grid>
    </div>
    <footer_nav></footer_nav>
  </div>
</template>

<script>
  import footer from '@/components/footer'
  import qs from 'qs';
  export default {
    data() {
      return {
        activeKey: 0,
        list: [

        ],
        arr: [

        ],
      };
    },
    components: {
      'footer_nav': footer
    },
    created: function() {
      this.why();
      this.mym(2);
    },
    methods: {
      why() {
        var _this = this;
        this.$axios.post('https://dawn.changxvan.top/api/Category/index', qs.stringify({

          }))
          .then(function(response) {
            console.log(response.data)
            _this.list = response.data.list;
          })
          .catch(function(error) {
            console.log(error);
          });
      },
      mym(id) {
        // id = 2;
        var _this = this;
        // alert(id)
        _this.id = id
        this.$axios.post('https://dawn.changxvan.top/api/Category/getcat', qs.stringify({
            cat_id: id
          }))
          .then(function(response) {
            console.log(response.data)
            _this.arr = response.data.catList;
          })
          .catch(function(error) {
            console.log(error);
          });
      },
      xq(id) {
        // alert(id),
        this.$router.push({
          name: 'product',
          query: {
            id: id
          }
        })
      }
    }
  }
</script>

<style scoped>
  /deep/ .van-grid-item__icon{
    font-size: 100px;
  }
</style>

<template>
  <div>
    <div class="carousel">
      <el-carousel :interval="4000" type="card" height="200px">
        <el-carousel-item v-for="item in imgList" :key="item">
          <img :src="'https://images.weserv.nl/?url=' + item" alt="" />
        </el-carousel-item>
      </el-carousel>
    </div>
    <div class="tab-list">
      <el-tabs v-model="activeName" :stretch=true @tab-click="changeList">
        <el-tab-pane label="虚构类" name="book_fiction"></el-tab-pane>
        <el-tab-pane label="非虚构类" name="book_nonfiction"></el-tab-pane>
      </el-tabs>
      <ul>
        <li class="book-item" v-for="book in bookList" :key="book.id">
          <div class="nr">
            <div class="img-box">
              <img
                :src="'https://images.weserv.nl/?url=' + book.cover.url"
                alt=""
              />
            </div>
            <div class="content">
              <h3>{{ book.title }}</h3>
              <p>{{ book.info }}</p>
              <el-rate
                :value ="book.rating.value/2"
                disabled
                show-score
                text-color="#ff9900"
                score-template="{value}"
              >
              </el-rate>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "Book",
  created() {
    this.getData();
  },
  data() {
    return {
      imgList: [],
      bookList: [],
      activeName:'book_fiction',
    };
  },
  methods: {
    getData() {
      this.axios
        .get(
          "https://bird.ioliu.cn/v2?url=https://m.douban.com/rexxar/api/v2/subject_collection/"+this.activeName+"/items?&start=0&count=8"
        )
        .then((res) => {
          console.log(res);
          this.bookList = res.data.subject_collection_items;
          this.imgList = this.bookList.map((item) => {
            return item.cover.url;
          });
        });
    },
    changeList() {
      
      this.getData();
    },
  },
};
</script>

<style lang="scss" scoped>
.el-carousel__item {
  img {
    width: 100%;
  }
}
.book-item .nr {
  display: flex;
  .img-box {
    flex: 3;
  }
  img {
    width: 100%;
  }

  .content {
    flex: 5;
    padding: 0.8rem;
    text-align: center;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    h3 {
      font-weight: bold;
    }
  }
}
.nr {
  padding: 10px 0;
  border-bottom: 1px solid black;
}
</style>
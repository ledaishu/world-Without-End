<template>
  <Card>
    <p slot="title">排行榜</p>
    <div slot="extra"></div>
    <div>
      <Tabs value="name1">
        <TabPane label="金币" name="name1">
          <p v-for="(item, idx) in leaderboardLst1" :key="idx">
            {{ ++idx }}: {{ item.name }}: {{ item.coin }}
          </p>
        </TabPane>
        <TabPane
          label="等级"
          name="name2"
          style="max-height: 424px; overflow: auto"
        >
          <p v-for="(item, idx) in leaderboardLst2" :key="idx">
            {{ ++idx }}: {{ item.name }}: {{ item.level }}
          </p>
        </TabPane>
        <TabPane label="铜币" name="name3">
          <p v-for="(item, idx) in leaderboardLst3" :key="idx">
            {{ ++idx }}: {{ item.name }}: {{ item.money }}
          </p>
        </TabPane>
        <TabPane label="天榜" name="name4">
          <p v-for="(item, idx) in leaderboardLst4" :key="idx">
            {{ ++idx }}: {{ item.name }}: {{ item.realmName }}
          </p>
        </TabPane>
        <TabPane label="地榜" name="name5">
          <p v-for="(item, idx) in leaderboardLst5" :key="idx">
            {{ ++idx }}: {{ item.name }}: {{ item.realmName }}
          </p>
        </TabPane>
      </Tabs>
    </div>
  </Card>
</template>
       
<script>
export default {
  name: "rankingList",
  data() {
    return {
      leaderboardLst1: [], // 金币排行榜列表
      leaderboardLst2: [], // 等级排行榜列表
      leaderboardLst3: [], // 铜币排行榜列表
      leaderboardLst4: [], // 天榜排行榜列表
      leaderboardLst5: [], // 地榜排行榜列表
    };
  },
  created() {
    this.leader();
    setInterval(() => {
      this.leader();
    }, 1000000);
  },
  methods: {
    // 列表
    leader() {
      // 金币排行榜
      this.$http.post("/gamepassport/coinRanking").then((res) => {
        this.leaderboardLst1 = res.data.data;
      });

      // 等级排行榜
      this.$http.post("/gamepassport/levelRanking").then((res) => {
        this.leaderboardLst2 = res.data.data;
      });
      // 铜币排行榜
      this.$http.post("/gamepassport/moneyRanking").then((res) => {
        this.leaderboardLst3 = res.data.data;
      });
      // 天榜排行榜
      this.$http.post("/gamepassport/realmHeavenList").then((res) => {
        this.leaderboardLst4 = res.data.data;
      });
      // 地榜排行榜
      this.$http.post("/gamepassport/realmLandList").then((res) => {
        this.leaderboardLst5 = res.data.data;
      });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>

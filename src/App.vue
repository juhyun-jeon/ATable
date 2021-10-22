<template>
  <div id="app">
    <button class="btn" @click="setDetailMode">Detail</button>
    <button class="btn" @click="setDetailMode">Edit</button>
    <div class="table-1">
      <a-table
        :columns="columns"
        :rows="rows"
        :height="height"
        :detail-mode="detailMode"
        @row-clicked="changeStock"
      />
    </div>
  </div>
</template>

<script>
import ATable from "./components/ATable";

export default {
  name: "App",
  components: {
    ATable,
  },
  data() {
    return {
      detailMode: false,
      editMode: false,
      columns: [
        {
          label: "",
          field: "code",
          thClass: "code-checkbox",
          tdClass: "code-checkbox",
          width: "50px",
        },
        {
          label: "종목명",
          subLabel: "세부사업군",
          field: "cname",
          subField: "factor",
          thClass: "cname",
          tdClass: "cname",
        },
        {
          label: "현재가",
          subLabel: "거래대금",
          field: "close",
          subField: "volume_valued",
          type: "number",
          tdClass: "text-color-apply",
          align: "right",
          width: "50px",
        },
        {
          label: "변동률",
          subLabel: "거래량",
          field: "returns",
          subField: "volume",
          type: "number",
          tdClass: "text-color-apply",
          align: "right",
          width: "80px",
        },
      ],
      rows: [
        {
          code: "155660",
          cname: "DSR",
          factor: "내구소비재및의류",
          image:
            "https://staging-file.alphasquare.co.kr/media/images/users/efbd7ba5158344648ca70255a0b801f2.jpeg",
          description:
            "해외 현지 법인을 관리 감독 및 운영 사업을 영위하는 주요 관계사인 DSR 제강의 홍하종 대표가 위스콘신 대학 MBA 출신이라는 점에 관련주로 부각",
          dt: 1634798397000,
          open: 8120,
          high: 8180,
          low: 7740,
          close: 7790,
          volume: 275264,
          volume_valued: 2165488430,
          returns: "-7.29%",
          prev_close: 8120,
        },
        {
          code: "099220",
          cname: "SDN",
          factor: "내구소비재및의류",
          image:
            "https://staging-file.alphasquare.co.kr/media/images/users/6b2d271342544792a1c72f75150e9e7a.jpeg",
          description:
            "최기혁 대표와 유승민 의원이 위스콘신 대학교 동문이라는 소식과 최기혁 대표가 위스콘신 동문회 부회장을 맡고 있다는 소식에 관련주로 부각",
          dt: 1634798397000,
          open: 2320,
          high: 2350,
          low: 2230,
          close: 2245,
          volume: 1156707,
          volume_valued: 2654521240,
          returns: "-7.29%",
          prev_close: 2295,
        },
        {
          code: "094190",
          cname: "이엘케이",
          factor: "내구소비재및의류",
          image: "",
          description:
            "신동혁 대표와 유승민 의원이 위스콘신대학 및 서울대 동문",
        },
        {
          code: "083470",
          cname: "이엠앤아이",
          factor: "내구소비재및의류",
          image:
            "https://staging-file.alphasquare.co.kr/media/images/users/6454db2266f74c65995f1087379b888c.png",
          description: "",
          dt: 1634798397000,
          open: 1390,
          high: 1390,
          low: 1390,
          close: 1390,
          volume: 0,
          volume_valued: 0,
          returns: "-7.29%",
          prev_close: 1390,
        },
        {
          code: "078590",
          cname: "OQP",
          factor: "내구소비재및의류",
          image: "",
          description:
            "경남 밀양에 본사가 위치해 있다는 소식에 유승민의 동남권 신공항 정책 수혜주로 부각",
          dt: 1634798397000,
          open: 2380,
          high: 2380,
          low: 2380,
          close: 2380,
          volume: 0,
          volume_valued: 0,
          returns: "-7.29%",
          prev_close: 2380,
        },
        {
          code: "069730",
          cname: "DSR제강",
          factor: "내구소비재및의류",
          image:
            "https://staging-file.alphasquare.co.kr/media/images/users/avatar/6583e1af-1b4b-4241-a82f-1d81d33ec018.jpg",
          description:
            "홍하종 대표가 위스콘신 대학 MBA 출신이라는 점에 관련주로 부각",
          dt: 1634798397000,
          open: 7960,
          high: 7960,
          low: 7300,
          close: 7300,
          volume: 450222,
          volume_valued: 3408799670,
          returns: "-7.29%",
          prev_close: 7880,
        },
        {
          code: "020180",
          cname: "대신정보통신",
          factor: "내구소비재및의류",
          image: "",
          description:
            "대신 정보통신 대표가 유승민 의원과 위스콘신 대 대학원 동문이라는 소식에 관련주로 부각되었음",
          dt: 1634798397000,
          open: 1450,
          high: 1455,
          low: 1380,
          close: 1420,
          volume: 1799191,
          volume_valued: 2544285695,
          returns: "-7.29%",
          prev_close: 1450,
        },
        {
          code: "013000",
          cname: "세우글로벌",
          factor: "내구소비재및의류",
          image: "",
          description: "테마 등록 사유",
          dt: 1634798397000,
          open: 3460,
          high: 3480,
          low: 3175,
          close: 3175,
          volume: 1671454,
          volume_valued: 5505542385,
          returns: "-7.29%",
          prev_close: 3485,
        },
        {
          code: "011370",
          cname: "서한",
          factor: "내구소비재및의류",
          image: "",
          description:
            "김진기 사외이사가 유승민 의원의 매형이라는 소식에 관련주로 부각",
          dt: 1634798397000,
          open: 2025,
          high: 2030,
          low: 1945,
          close: 1960,
          volume: 1522425,
          volume_valued: 2994455165,
          returns: "-7.29%",
          prev_close: 2030,
        },
        {
          code: "007530",
          cname: "영신금속",
          factor: "내구소비재및의류",
          image: "",
          description:
            "영신금속의 이정우 대표가 위스콘신 대학원 출신으로 유승민 의원과 동문이라는 소식에 관련주로 부각",
          dt: 1634798397000,
          open: 2985,
          high: 3010,
          low: 2955,
          close: 2955,
          volume: 34176,
          volume_valued: 101825070,
          returns: "-7.29%",
          prev_close: 2985,
        },
        {
          code: "004780",
          cname: "대륙제관",
          factor: "내구소비재및의류",
          image: "",
          description:
            "박봉준 사장이 위스콘신 메디슨 대학 MBA 출신으로 유승민 의원과 동문이라는 소식에 관련주로 부각되었음",
          dt: 1634798397000,
          open: 5730,
          high: 5810,
          low: 5690,
          close: 5750,
          volume: 136058,
          volume_valued: 781386700,
          returns: "-7.29%",
          prev_close: 5820,
        },
      ],
      height: "3.6rem",
    };
  },
  methods: {
    setDetailMode() {
      this.detailMode = !this.detailMode;
      if (this.detailMode) this.height = "5.2rem";
      else this.height = "3.6rem";
    },
    setEditMode() {
      this.editMode = !this.editMode;
    },
    changeStock(i) {
      console.log(i);
    },
  },
};
</script>

<style lang="scss" scoped>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin-top: 10px;
}

.table-1 {
  width: 40rem;
  height: 50rem;
}

.btn {
  width: 5rem;
  height: 2rem;
  margin: 0 1rem;
  border-radius: 4px;
  background-color: aquamarine;
}
</style>

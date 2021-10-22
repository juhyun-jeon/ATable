<template>
  <div class="a-table">
    <div class="a-table__head">
      <div class="a-table__column" :style="{ height: height }">
        <div
          class="a-table__column-item"
          v-for="(item, idx) in columns"
          :key="item.field"
          :class="getClass(idx)"
          :style="getStyle(idx)"
        >
          <label
            @click.stop
            v-if="item.field === 'code'"
            class="a-table__select-checkbox"
          >
            <input
              class="a-table__select-input"
              type="checkbox"
              @change="selectAll"
              :checked="checked.length === test.length"
            />
            <CheckBoxIcon :width="20" :height="20" />
          </label>
          <div v-else>
            <p>{{ item.label }}</p>
            <p
              class="a-table__column-item-sub"
              v-if="detailMode && item.subLabel"
            >
              {{ item.subLabel }}
            </p>
          </div>
        </div>
      </div>
    </div>
    <div class="a-table__body">
      <div
        class="a-table__row"
        :style="{ height: height }"
        v-for="(row, idx) in rows"
        :key="row.code"
        @click="onClickRow(idx)"
      >
        <div
          class="a-table__row-item"
          v-for="(item, idx) in columns"
          :key="item.field"
          :class="getClass(idx)"
          :style="getStyle(idx)"
        >
          <label
            @click.stop
            v-if="item.field === 'code'"
            class="a-table__select-checkbox"
          >
            <input
              v-model="checked"
              class="a-table__select-input"
              type="checkbox"
              :value="row.code"
              @change="onChange"
            />
            <CheckBoxIcon :width="20" :height="20" />
          </label>
          <img v-else-if="item.field === 'image'" src="row[item.field]" />
          <div v-else>
            <p>{{ row[item.field] }}</p>
            <p v-if="detailMode && item.subLabel" class="a-table__row-item-sub">
              {{ row[item.subField] }}
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import CheckBoxIcon from "../icons/CheckBoxIcon.vue";
export default {
  components: { CheckBoxIcon },
  props: {
    columns: {
      type: Array,
      required: true,
    },
    rows: {
      type: Array,
      required: true,
    },
    height: {
      type: String,
      default: "2rem",
    },
    detailMode: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {
      test: [],
      checked: [],
    };
  },
  created() {
    this.test = this.rows.map((item) => item.code);
  },
  methods: {
    getClass(idx) {
      return [this.columns[idx].thClass, this.columns[idx].align];
    },
    getStyle(idx) {
      const style = {};
      if (this.columns[idx].width) style["width"] = this.columns[idx].width;
      else style["flex"] = 1;
      if (this.columns[idx].align)
        style["text-align"] = this.columns[idx].align;
      return style;
    },
    onClickRow(i) {
      this.$emit("row-clicked", i);
    },
    onChange() {
      console.log(this.checked);
    },
    selectAll() {
      if (this.checked.length === this.test.length) this.checked = [];
      else this.checked = this.test;
    },
  },
};
</script>

<style lang="scss">
.a-table {
  width: 100%;
  height: 100%;
  .a-table__column,
  .a-table__row {
    padding: 0 10px;
    display: flex;
    align-items: center;
    position: relative;
  }
  .a-table__row:hover {
    cursor: pointer;
    background-color: #f1f0f0;
  }
  .a-table__column-item {
    font-size: 1.4rem;
    line-height: 2rem;
    color: #646464;
    .a-table__column-item-sub {
      font-size: 1.2rem;
      line-height: 1.6rem;
    }
  }
  .a-table__row-item {
    font-size: 1.4rem;
    line-height: 2rem;
    .a-table__row-item-sub {
      font-size: 1.3rem;
      line-height: 1.6rem;
      color: #646464;
    }
  }
  .a-table__select-checkbox {
    display: block;
    .a-table__select-input {
      position: absolute;
      opacity: 0;
      cursor: pointer;
      height: 0;
      width: 0;
      &:checked ~ {
        .check-box-icon {
          color: #dd2626;
          .check-box-icon__background {
            fill: #dd2626;
          }
        }
      }
    }
    .check-box-icon {
      position: absolute;
      top: 0.8rem;
      left: 1.8rem;
      cursor: pointer;
    }
  }
}

html,
body,
div,
span,
applet,
object,
iframe,
button,
h1,
h2,
h3,
h4,
h5,
h6,
p,
blockquote,
pre,
a,
abbr,
acronym,
address,
big,
cite,
code,
del,
dfn,
em,
img,
ins,
kbd,
q,
s,
samp,
small,
strike,
strong,
sub,
sup,
tt,
var,
b,
u,
i,
center,
dl,
dt,
dd,
ol,
ul,
li,
fieldset,
form,
label,
legend,
table,
caption,
tbody,
tfoot,
thead,
tr,
th,
td,
article,
aside,
canvas,
details,
embed,
figure,
figcaption,
footer,
header,
hgroup,
menu,
nav,
output,
ruby,
section,
summary,
time,
mark,
audio,
video {
  margin: 0;
  padding: 0;
  border: 0;
  font-size: 100%;
  font: inherit;
  text-decoration: none;
}

html,
body {
  width: 100%;
  height: 100%;
  font-size: 62.5%;
  overflow: hidden;
}

*,
:after,
:before {
  box-sizing: border-box;
}

tspan {
  font-family: AlphaSans, sans-serif !important;
}

:focus,
button.active.focus,
button.active:focus,
button.focus,
button:active.focus,
button:active:focus,
button:focus {
  outline: 0;
}

/* HTML5 display-role reset for older browsers */
article,
aside,
details,
figcaption,
figure,
footer,
header,
hgroup,
menu,
nav,
section {
  display: block;
}

body {
  line-height: 1;
}

table {
  width: 100%;
  max-width: 100%;
  border-collapse: collapse;
  border-spacing: 0;
  > tbody > tr > td,
  > tbody > tr > th,
  > tfoot > tr > td,
  > tfoot > tr > th,
  > thead > tr > td,
  > thead > tr > th {
    line-height: 1.42857143;
  }
}

ul,
ol,
li,
a {
  list-style: none;
}

h1,
h2,
h3,
h4,
h5,
h6 {
  word-break: keep-all;
}

p,
label {
  word-break: keep-all;
  margin-bottom: 0;
}

textarea {
  font: inherit;
}

// 크로스브라우징을 지원하는 범용적 button 초기화 css
button {
  display: inline-block;
  font-family: inherit;
  vertical-align: middle;
  cursor: pointer;
  white-space: nowrap;
  text-decoration: none;
  background: transparent;
  border: 0;
}
</style>

<template>
  <li class="line">
    <p class="sep" v-if="cmd !== 'welcome'">
      <span class="user">{{ user }}</span>@<span class="domain">{{ domain }}</span><span class="directory">:{{ dir }}</span> <span class="tick">%</span>
      <small>{{ cmd }}</small>
    </p>
    <ul :class="cmd">
      <li v-for="(item, index) in response" :key="index">
        <pre v-html="item"></pre>
      </li>
    </ul>
  </li>
</template>

<script>
export default {
  name: 'CommandLine',
  props: ['user', 'dir', 'domain', 'cmd'],
  data: function () {
    return {
      response: this.$parent.run(this.user, this.cmd)
    }
  }
}
</script>

<style lang="scss">
@import '../assets/colors';
.line {
  ul:not(.welcome) { margin-left: 2px }
  p, pre { white-space: pre-wrap }
  a {
    text-decoration: none;
    padding: 0 2px;
  }
}
.sep { margin: 0.5rem 0 }
.ascii { color: $grey }
span { color: $purple }
.command { color: $yellow }
.user { color: $red }
.tick { color: $blue; margin: 0 0.5rem; font-size: 12px }
.domain { color: $grey }
.directory { color: $blue }
.light { font-weight: normal; font-style: italic; }
.welcome { line-height: 1rem; }
</style>

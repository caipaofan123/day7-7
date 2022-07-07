<template>
  <div>
    {{ str }}
    <br />
    <input type="text" v-show="true" v-gfocus v-number="qwe" v-model="str" />
    <p v-color="colorstr" @click="colorstr='red'">ewdwefcaw</p>
  </div>
</template>

<script>
export default {
  name: 'New7Directive',

  data() {
    return {
      str: '',
      colorstr:'green',
      qwe:''
    };
  },
  directives: {
    focus: {
      inserted(el) {
        console.log(el);
        el.focus();
      },
    },
    number: {
      inserted(el,binding,vnode) {
        console.log(binding.expression);
        el.value = el.value.replace(/[^\d.]/g, '');
        vnode.context[binding.expression]=el.value
      },
      update(el,binding,vnode) {
        el.value = el.value.replace(/[^\d.]/g, '');
        vnode.context[binding.expression]=el.value
      },
    },
    color: {
      inserted(el, bind) {
        el.style.color = bind.value;
      },
      update(el, bind) {
        el.style.color = bind.value;
      },
    },
  },
  mounted() {},

  methods: {},
};
</script>

<style lang="scss" scoped></style>

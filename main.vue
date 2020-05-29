<template>
  <div class="wrapper">
    <div ref="blacksquare" class="bs">{{ range.toFixed() }}%</div>
    <section>
      <h1>Section 1</h1>
    </section>
    <section class="s2">
      <h1>Section 2</h1>
    </section>
    <section>
      <h1>Section 3</h1>
    </section>
  </div>
</template>

<script>
export default {
  data: () => ({ range: 0, animation: null }),
  mounted() {
    this.animation = anime({
      targets: this.$refs.blacksquare,
      // right: 0,
      translateX: function (el) {
        return (
          document.body.getBoundingClientRect().width -
          el.getBoundingClientRect().width
        );
      },
      rotate: "2turn",
      autoplay: false,
      easing: "linear"
    });
    window.addEventListener("scroll", () => {
      this.range = this.getScrollPercent();
    });
    // init
    this.range = this.getScrollPercent();
  },
  watch: {
    range: function (val) {
      this.animation.seek(this.animation.duration * (val / 100));
    }
  },
  methods: {
    getScrollPercent() {
      const d = document.documentElement;
      return (d.scrollTop / (d.scrollHeight - d.clientHeight)) * 100;
    }
  }
};
</script>

<style>
body {
  font-family: Montserrat;
}

section {
  min-height: 100vh;
  text-align: center;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.bs {
  position: fixed;
  top: calc(50% - 30px);
  background-color: black;
  width: 60px;
  height: 60px;
  color: white;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  font-weight: 700;
}

.s2 {
  background-color: #f2f2f2;
}
</style>

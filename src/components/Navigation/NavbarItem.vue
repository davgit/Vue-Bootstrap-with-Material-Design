<template>
  <component :is="tag" :class="className" @click="(e) => handleClick(e)" ref="navItem">
    <router-link
      tag="a"
      v-if="to"
      :exact="exact"
      active-class="active"
      exact-active-class="active"
      :class="anchorClassName"
      :to="to"
      :target="tab"
    >
      <mdb-icon v-if="icon" :far="far" :fab="fab" :fad="fad" :fal="fal" :icon="icon" />
      <span v-if="icon" class="clearfix d-none d-sm-inline-block">
        <slot></slot>
      </span>
      <slot v-else></slot>
    </router-link>
    <a v-else :href="href" :class="anchorClassName" :target="tab">
      <mdb-icon v-if="icon" :far="far" :fab="fab" :fad="fad" :fal="fal" :icon="icon" />
      <span v-if="icon" class="clearfix d-none d-sm-inline-block">
        <slot></slot>
      </span>
      <slot v-else></slot>
    </a>
  </component>
</template>

<script>
import waves from "../../mixins/waves";
import mdbIcon from "../Content/Fa";

const NavbarItem = {
  components: {
    mdbIcon
  },
  props: {
    tag: {
      type: String,
      default: "li"
    },
    active: {
      type: Boolean,
      default: false
    },
    disabled: {
      type: Boolean
    },
    exact: {
      type: Boolean,
      default: false
    },
    href: {
      type: String
    },
    newTab: {
      type: Boolean,
      default: false
    },
    to: [String, Object],
    waves: {
      type: Boolean,
      default: true
    },
    anchorClass: {
      type: String
    },
    icon: {
      type: String
    },
    far: {
      type: Boolean,
      default: false
    },
    fab: {
      type: Boolean,
      default: false
    },
    fad: {
      type: Boolean,
      default: false
    },
    fal: {
      type: Boolean,
      default: false
    },
  },
  data() {
    return {
      isNavFixed: false
    };
  },
  computed: {
    className() {
      return ["nav-item", this.waves && "ripple-parent"];
    },
    anchorClassName() {
      return [
        {
          "nav-link": true,
          "navbar-link": true,
          disabled: this.disabled,
          active: this.active
        },
        this.anchorClass
      ];
    },
    tab() {
      if (this.newTab) {
        return "_blank";
      }
      return false;
    }
  },
  methods: {
    handleClick(e) {
      this.$emit("click", e);
      this.wave(e);
    }
  },
  mounted() {
    let el = this.$refs.navItem;
    while (el.parentNode) {
      if (el.className.includes("fixed")) {
        this.isNavFixed = true;
        break;
      }
      el = el.parentNode;
    }
  },
  mixins: [waves]
};

export default NavbarItem;
export { NavbarItem as mdbNavItem };
</script>

<style scoped>
</style>

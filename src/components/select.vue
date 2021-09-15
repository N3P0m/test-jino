<template>
  <div class="select">
    <div class="select__selected" tabindex="0" @click="show = !show" @keydown="navigationKeys" ref="select">
      <svg class="select__selected-arrow"
      :class="{'select__selected-arrow--active' : show}"
       width="10" height="6" viewBox="0 0 10 6" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path d="M0.333163 4.92493C0.332938 4.82718 0.352328 4.73037 0.390205 4.64011C0.428083 4.54985 0.483694 4.46794 0.553806 4.39915L4.47726 0.547848C4.61709 0.410389 4.80613 0.333252 5.00315 0.333252C5.20017 0.333252 5.3892 0.410389 5.52904 0.547848L9.44586 4.39258C9.58643 4.53072 9.66584 4.7185 9.66662 4.91463C9.6674 5.11076 9.58948 5.29915 9.45 5.43838C9.31053 5.57761 9.12092 5.65626 8.9229 5.65703C8.72487 5.6578 8.53465 5.58063 8.39407 5.44249L4.99983 2.11203L1.60559 5.44906C1.5009 5.55197 1.36778 5.62185 1.22303 5.6499C1.07827 5.67795 0.928375 5.6629 0.79225 5.60665C0.656125 5.5504 0.539873 5.45548 0.458167 5.33386C0.376462 5.21223 0.332964 5.06937 0.333163 4.92329L0.333163 4.92493Z" fill="#9C9C9C"/>
      </svg>
      <p class="select__selected-group">{{grName || defaultName}}</p>
      <p class="select__selected-name">{{defaultValue}}</p>
    </div>
    <div class="select__list" v-show="show" >
      <p class="select__item select__item--default" 
      @click="selectedDefault"
      @keydown="selectedDefault"
      ref="defaultSelected"
      tabindex="0">
      {{nothingValue}}
      </p>
      <div class="select__group"
      v-for="option in options" 
      :key="option.id">
        <p v-if="option.group" class="select__group-name"
        @click="selected(option)"
        >
          {{ option.group }}
        </p>
        <p class="select__item" v-for="item in option.groupValues" :key="item.id" @click="selected(item, option)" @keydown="selected(item, option)"   :ref="arrItems" tabindex="0">{{item.name}}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    defaultName: {
      type: String,
      required: true,
    },
    options: {
      type: Array,
      default() {
        return [];
      },
    },
  },
  data() {
    return {
      defaultValue: "Выберете",
      nothingValue: "Ничего не выбирать",
      grName: "",
      show: false,
      selectArr: [],
    };
  },
  methods: {
    selected(item, option) {
      if (event.code == "Space" || event.pointerId == "1") {
        this.selectArr.forEach(el => el.style.backgroundColor = "#ffffff")
        event.target.style.background = '#F7F7F7'
        this.defaultValue = item.name
        option.group = true ? this.grName = option.group : this.grName
        this.show = false
        this.$refs.select.focus()
        this.$refs.defaultSelected.style.backgroundColor = "#ffffff"
      }

    },
    selectedDefault() {
       if (event.code == "Space" || event.pointerId == "1") {
         this.defaultValue = "Выберете"
         this.selectArr.forEach(el => el.style.backgroundColor = "#ffffff")
         event.target.style.backgroundColor = "#F7F7F7"
         this.show = false
       }
    },
    focus() {
      event.target.focus()
    },
    arrItems(el) {
      this.selectArr.push(el)
    },
    navigationKeys(event) {
      if (event.code == 'Space') this.show = !this.show
      console.log(event.code)
   
    },
    closeSelect() {
      if (!event.target.closest('.select')) {
        this.show = false
      }
    }
    

  },
  mounted() {
    document.addEventListener('click', this.closeSelect)
  },
  unmounted() {
    document.removeEventListener('click', this.closeSelect)
  },
};
</script>

<style lang="scss" scoped>
.select {
  position: relative;
  width: 300px;
  color: #333;

  &__selected {
    position: relative;
    padding: 8px 16px 2px 16px;
    border: 1px solid #ccc;
    margin: 0;
    width: 100%;
    box-sizing: border-box;
    border-radius: 10px ;
    cursor: pointer;
    text-align: start;

    &:focus {
      outline: none;
      box-shadow: 0 0 0 1px #59ce65,
      0 0 0 4px #e7ffe9 ;
      }

  &-group {
    padding: 0;
    margin: 0;
    font-size: 13px;
    line-height: 16px;
    color: #5F6062;
  }

  &-name {
    padding: 0;
    margin: 0;
    font-size: 16px;
    line-height: 24px;
  }
    
  &-arrow {
    position: absolute;
    top: 21px;
    right: 20px;
    transform: rotateX(180deg);
    transition: 0.3s;

    &--active {
      transform: rotateX(0deg);
    }
  }

  }

  &__list {
    position: absolute;
    border-radius: 10px;
    top: 150%;
    right: 0;
    width: 100%;
    box-sizing: border-box;
    box-shadow: 0px 4px 20px rgba(0, 0, 0, 0.16);
    overflow: hidden;
  }

  &__item{
    margin: 0;
    padding: 12px 8px;
    margin: 8px;
    border-radius: 4px;
    cursor: pointer;
    text-align: start;

    &:hover {
      background-color: #ebebeb !important;
    }

    &:focus {
      outline: none;
      background-color: #ebebeb !important;
    }

    &--default {
      background-color: #f7f7f7;
    }
  }

  &__group {
    border-top: 1px solid #EBEBEB;

    &-name {
      color: #5F6062;
      text-align: start;
      font-weight: 700;
      padding: 8px 12px;
      margin: 4px 0 0 0;
    }
  }
}
</style>

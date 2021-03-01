<template>
  <Layout>
    <div class="tags">
      <router-link class="tag"
                   v-for="tag in tags" :key="tag.id"
                   :to="`/labels/edit/${tag.id}`">
        <span>{{ tag.name }}</span>
        <Icon name="right"/>
      </router-link>
    </div>
    <div class="createTagWrapper">
      <Button class="createTag" @click="createTag">新建标签</Button>
    </div>
  </Layout>
</template>

<script lang="ts">
import Vue from 'vue'
import {Component} from 'vue-property-decorator'
import Button from '@/components/Button.vue'
import {mixins} from 'vue-class-component'
import TagHelper from '@/mixins/TagHelper'

@Component({
  components: {Button}
})
export default class Labels extends mixins(TagHelper) {
  get tags() {
    return this.$store.state.tagList
  }

  beforeCreate() {
    this.$store.commit('fetchTags')
  }
}
</script>

<style lang="scss" scoped>
.tags {
  background: white;
  padding-left: 16px;
  font-size: 16px;

  > .tag {
    min-height: 44px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    border-bottom: 1px solid #e8e8e8;

    svg {
      width: 16px;
      height: 16px;
      color: #666;
      margin-right: 16px;
    }
  }
}

.createTag {
  background: lightskyblue;
  color: #333;
  border-radius: 4px;
  border: none;
  height: 40px;
  padding: 0 16px;

  &Wrapper {
    text-align: center;
    padding: 16px;
    margin-top: 28px;
  }
}
</style>
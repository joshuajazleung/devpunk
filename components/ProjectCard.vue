<template>
<div class="col-md-6 col-lg-3 col-xs-12 cardLayout-outer" data-toggle="modal" :data-target="'#' + project.id">
  <div class="card">
    <img :src="project.thumbnails.small[0]" 
         class="card-img-top"
         :srcset="`${project.thumbnails.high[0]} 1400w, ${project.thumbnails.medium[0]} 900w, ${project.thumbnails.small[0]} 400w`"
         sizes="(min-width: 991px) 25vw, (min-width: 768px) 50vw, 100vw" 
         width="100%"
         :alt="project.title">
    <div class="card-block">
      <h4 class="card-title"><span class="card-subtitle">{{ upcaseTitle(project.subtitle) }}</span>{{ upcaseTitle(project.title) }}</h4>
      <p class="card-text" v-html="shortDescription(project.description)"></p>
      <button type="button" class="btn btn-custom btn-grapefruit" data-toggle="modal" :data-target="'#' + project.id">CHECK OUT</button>
      <modal :modal-id="project.id" :project="project"></modal>
    </div>
  </div>
</div>
</template>

<script>
import Modal from './Modal'
// import _ from 'lodash'

export default {
  name: 'ProjectCard',
  props: ['project'],
  components: {
    Modal
  },
  methods: {
    shortDescription(body) {
      return _.truncate(body, { 
                                length: 100,
                                separator: ' '
                              })
    },
    upcaseTitle(title) {
      return _.toUpper(title);
    }
  },
}
</script>

<style scoped>
.card-subtitle {
  display: block;
  font-size: 0.9rem;
  margin-bottom: 0.5rem;
  font-weight: 700;
  color: #9b9b9b;
}
.preview {
  width: 100%;
}
</style>
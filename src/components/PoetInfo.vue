<template>
    <div>
        <div class="poet-info__wrapper">
            <div class="poet-info_title">
                <h1>You are</h1>
                <h2>{{poetData.title}}</h2>
            </div>
            <div class="poet-info_avatar">
                <img :src="poetData.originalimage.source" width="230" height="285"/>
            </div>
            <div class="poet-info_body" v-html="poetData.extract_html">
                {{poetData.extract_html}}
            </div>
        </div>
    </div>
</template>

<script>
export default {
  props: ['poetData'],
  data() {
    return {};
  },
};
</script>

<style scoped>
    .poet-info__wrapper {
        text-align: center;
    }
    .poet-info_body, .poet-info_avatar {
        padding-top: 10px;
    }
</style>

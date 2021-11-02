<template>
  <div class="repo">
        <a :href="repoUrl" class="repo-name"><i class='bx bx-link-alt'></i> {{ repoName }}</a>
        <p class="repo-desc">{{ repoDesc }}</p>
        <div class="repo-tags">
          <span class="tags views"><i class='bx bxs-show'></i> {{ views }}</span>
          <span class="tags star"><i class='bx bxs-star' ></i> {{ star }} </span>
          <span class="tags info"><i class='bx bx-info-circle'></i> {{ info }} </span>
          <span class="tags meal"><i class='bx bxs-show'></i> {{ fork }} </span>
        </div>
      </div>
</template>

<script>
export default {
    name: "UserRepoCard",
    props:{
        repoName:{
            type: String,
            Required: false,
            default: "Github repo"
        },
        repoDesc: {
            type: String,
        },
        repoUrl: {
            type: String
        },
        views: {
            type: Number
        },
        star: {
            type: Number
        },
        info: {
            type: Number
        },
        fork: {
            type: Number
        },
    }
}
</script>

<style lang="scss" scoped>
.repo{
      width: 100%;
      padding: 15px;
      box-shadow: 0 3px 13px rgba($color: #000000, $alpha: .25);
      border-radius: 10px;
      border: 1px solid #aaa;
      margin-bottom: 25px;

      &-name{
        font-size: 1.1rem;
        text-decoration: none;
        color: #00ba66; 
        display: flex;
        align-items: center;

        &:hover{
          text-decoration: underline;
        }
        i{
          margin-right: 5px;
        }
      }
      &-desc{
        font-size: .9rem;
        padding: 0 20px;
      }
      &-tags{
        margin-top: 10px;
        padding-left: 20px;

        .tags{
          font-size: .8rem;
          padding: 2px 10px;
          margin-right: 10px;
          border-radius: 50px;
          display: inline-flex;
          align-items: center;

          &.views{
            background: rgba($color: #aa2222, $alpha: .4);
            border: 1px solid #a20404;
            color: #000;
          }
          &.star{
            background: rgba($color: #2c869d, $alpha: .4);
            border: 1px solid #0a819e;
            color: #000;
          }
          &.info{
            background: rgba($color: #aa2222, $alpha: .4);
            border: 1px solid #a20404;
            color: #000;
          }
          &.meal{
            background: rgba($color: #aa2222, $alpha: .4);
            border: 1px solid #a20404;
            color: #000;
          }

          i{
            margin-right: 5px;
          }
        }
      }
    }
</style>
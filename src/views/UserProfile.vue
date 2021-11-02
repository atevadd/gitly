<template>
  <div class="user-wrapper">
    <div class="profile-details">
      <div class="img">
        <img :src="userDetails.avatar_url" :alt="userDetails.login" />

        <div class="user-name">
          <h2>{{ userDetails.name }}</h2>
          <p>{{ userDetails.login }}</p>
        </div>
      </div>
      <div class="content">
        <div class="headline">
          <h3>{{ userDetails.name }}</h3>
          <span class="user-type">{{ userDetails.type }}</span>
          <span class="work-type" v-if="userDetails.hireable">Hirable</span>
        </div>
        <div class="desc">
          <h3>
            {{ userDetails.bio }}
          </h3>
        </div>
        <div class="meta-details">
          <ul>
            <li><i class="bx bx-map"></i>{{ userDetails.location }}</li>
            <li>
              <i class="bx bx-globe"></i
              ><a :href="userDetails.blog">{{ userDetails.blog }}</a>
            </li>
          </ul>
        </div>
      </div>
    </div>

    <div class="activity-details">
      <div class="activity">
        <p>Followers</p>
        <h1>{{ userDetails.followers }}</h1>
      </div>
      <div class="activity">
        <p>Following</p>
        <h1>{{ userDetails.following }}</h1>
      </div>
      <div class="activity">
        <p>Public Repo</p>
        <h1>{{ userDetails.public_repos }}</h1>
      </div>
      <div class="activity">
        <p>Public Gists</p>
        <h1>{{ userDetails.public_gists }}</h1>
      </div>
    </div>

    <div class="repositories">
      <h1>Top repositories</h1>
      <div class="show" v-if="userRepos">
        <UserRepoCard
          v-for="repo in userRepos"
          :repoName="repo.name"
          :repoUrl="repo.html_url"
          :repoDesc="repo.description"
          :views="repo.watchers_count"
          :star="repo.stargazers_count"
          :fork="repo.forks"
          :info="repo.open_issues_count"
          :key="repo.id"
        />
      </div>
    </div>
  </div>
</template>

<script>
import UserRepoCard from "@/components/UserRepoCard.vue";
import axios from "axios";

export default {
  name: "UserProfile",
  components: {
    UserRepoCard,
  },
  props: {
    userName: {
      type: String,
    },
  },
  emits:['search'],
  data() {
    return {
      userDetails: null,
      userRepos: null,
      clientId: "0ed705e5815fa23fa13b",
      clientSecret: "95eb90d8af643bd97c02dc881c2c38e5e91adb65",
    };
  },
  methods: {
    userInformation() {
      axios
        .get(
          `https://api.github.com/users/${this.userName}?client_id=${this.clientId}&client_secret=${this.clientSecret}`
        )
        .then((response) => {
          this.userDetails = response.data;
          console.log(response.data);
        })
        .catch((err) => {
          console.log(err.message);
        });
    },
    repoInformation() {
      axios
        .get(`https://api.github.com/users/${this.userName}/repos`)
        .then((response) => {
          this.userRepos = response.data.splice(0, 3);
          console.log(this.userRepos);
        });
    },
  },
  // mounted(){
  //   // this.userInformation()
  //   // this.repoInformation()
  // }
  beforeMount() {
    this.userInformation();
    this.repoInformation();
  },
};
</script>

<style lang="scss" scoped>
.user-wrapper {
  width: 80%;
  position: relative;
  display: block;
  margin: 20px auto;

  @media screen and (max-width: 480px) {
    width: 95%;
  }

  .profile-details {
    position: relative;
    display: grid;
    grid-template-columns: 20% minmax(0, 80%);
    gap: 30px;

    @media screen and (max-width: 480px) {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
    }

    .img {
      // border: 1px solid red;
      position: relative;
      width: 100%;
      height: 200px;

      img {
        // border: 1px solid red;
        width: 100%;
        height: 100%;
        object-fit: cover;
      }
    }

    .user-name {
      position: absolute;
      bottom: 0;
      left: 0;
      width: 100%;
      background: rgba(0, 0, 0, 0.45);
      padding: 10px;

      h2 {
        font-size: 0.9rem;
        color: #fff;
      }
      p {
        font-size: 0.8rem;
        color: #fff;

        @media screen and (max-width: 480px) {
          font-size: 0.75rem;
        }
      }
    }

    .content {
      position: relative;

      .headline {
        display: flex;
        align-items: center;
        margin-bottom: 10px;

        h3 {
          margin-right: 18px;
          font-size: 1.5rem;
        }
        span {
          font-size: 0.8rem;
          padding: 2px 10px;
          margin-right: 10px;
          border-radius: 50px;

          &.user-type {
            background: rgba($color: #007e3f, $alpha: 0.4);
            border: 1px solid #004120;
            color: #000;
          }
          &.work-type {
            background: rgba($color: #aa2222, $alpha: 0.4);
            border: 1px solid #a20404;
            color: #000;
          }
        }
      }
      .desc {
        position: relative;

        h3 {
          font-weight: 500;
          font-size: 1rem;

          @media screen and (max-width: 480px) {
            font-size: 0.88rem;
          }
        }
      }
      .meta-details {
        position: relative;
        margin-top: 7px;

        ul {
          list-style-type: none;
          display: flex;

          li {
            margin-right: 25px;
            font-size: 0.88rem;

            i {
              vertical-align: middle;
              margin-right: 5px;
            }
            a {
              color: #42b983;
              text-transform: capitalize;
            }
          }
        }
      }
    }
  }

  .activity-details {
    position: relative;
    width: 80%;
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin: 30px 0;

    @media screen and (max-width: 480px) {
      display: grid;
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: 30px;
      // border: 1px solid red;
      width: 100%;
    }

    .activity {
      border-left: 2px solid #aaa;
      padding-left: 15px;

      &:nth-child(1) {
        border: none;

        @media screen and (max-width: 480px) {
          border-left: 1px solid #aaa;
        }
      }
      p {
        font-size: 0.9rem;
      }
    }
  }

  .repositories {
    position: relative;
    width: 100%;
    display: block;
    margin-top: 40px;

    h1 {
      margin-bottom: 10px;

      @media screen and (max-width: 480px) {
        font-size: 1.4rem;
      }
    }

    .repo {
      width: 100%;
      padding: 15px;
      box-shadow: 0 3px 13px rgba($color: #000000, $alpha: 0.25);
      border-radius: 10px;
      border: 1px solid #aaa;
      margin-bottom: 25px;

      &-name {
        font-size: 1.1rem;
        text-decoration: none;
        color: #00ba66;
        display: flex;
        align-items: center;

        &:hover {
          text-decoration: underline;
        }
        i {
          margin-right: 5px;
        }
      }
      &-desc {
        font-size: 0.9rem;
        padding: 0 20px;
      }
      &-tags {
        margin-top: 10px;
        padding-left: 20px;

        .tags {
          font-size: 0.8rem;
          padding: 2px 10px;
          margin-right: 10px;
          border-radius: 50px;
          display: inline-flex;
          align-items: center;

          &.views {
            background: rgba($color: #aa2222, $alpha: 0.4);
            border: 1px solid #a20404;
            color: #000;
          }
          &.star {
            background: rgba($color: #2c869d, $alpha: 0.4);
            border: 1px solid #0a819e;
            color: #000;
          }
          &.info {
            background: rgba($color: #aa2222, $alpha: 0.4);
            border: 1px solid #a20404;
            color: #000;
          }
          &.meal {
            background: rgba($color: #aa2222, $alpha: 0.4);
            border: 1px solid #a20404;
            color: #000;
          }

          i {
            margin-right: 5px;
          }
        }
      }
    }
  }
}
</style>
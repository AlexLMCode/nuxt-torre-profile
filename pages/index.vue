<template>
  <main class="container">
    <nav-bar @showInput="show" />
    <search-modal
      v-if="active"
      :searchVal="searchInput"
      @searchValue="getSearchUser"
    />
    <Loading v-if="$fetchState.pending" />
    <div v-else>
      <div class="cover-image-container">
        <CoverImage :img="userInfo.picture" />
      </div>
      <div class="user-name">
        <h1>
          {{ userInfo.username }}
          <span v-if="userInfo.verified">
            <img src="../static/verif.svg" alt="verified" />
          </span>
        </h1>

        <p class="user-job">{{ userInfo.job }}</p>
        <p class="user-description">
          {{ userInfo.description }}
        </p>
      </div>

      <div class="info-container">
        <p class="info-title">Skills and interests:</p>
        <section class="info-container-grid">
          <div class="master info">
            <div class="info-img">
              <img src="../static/master.svg" alt="master icon" />
              <p>Master / Influencer</p>
            </div>
            <div class="skills">
              <Skill
                v-for="(skill, index) in master"
                :key="index"
                class="skills"
                :skill-name="skill.name"
              />
            </div>
          </div>

          <div class="expert info">
            <div class="info-img">
              <img src="../static/expert.svg" alt="expert icon" />
              <p>Expert</p>
            </div>

            <div class="skills">
              <Skill
                v-for="(skill, index) in expert"
                :key="index"
                class="skills"
                :skill-name="skill.name"
              />
            </div>
          </div>

          <div class="proficent info">
            <div class="info-img">
              <img src="../static/proficent.svg" alt="proficent icon" />
              <p>Proficent</p>
            </div>

            <div class="skills">
              <Skill
                v-for="(skill, index) in proficent"
                :key="index"
                :skill-name="skill.name"
              />
            </div>
          </div>

          <div class="novice info">
            <div class="info-img">
              <img src="../static/novice.svg" alt="novice icon" />
              <p>Novice</p>
            </div>
            <div class="skills">
              <Skill
                v-for="(skill, index) in novice"
                :key="index"
                class="skills"
                :skill-name="skill.name"
              />
            </div>
          </div>
        </section>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  name: 'IndexPage',

  data() {
    return {
      proficent: [],
      novice: [],
      expert: [],
      master: [],
      userInfo: {
        userName: '',
        job: '',
        description: '',
        picture: '',
        verified: false,
      },
      active: false,
      searchInput: 'alelujanmerino',
    }
  },
  async fetch() {
    await this.getInfo(this.searchInput)
  },

  methods: {
    async getInfo(username) {
      const { data } = await this.$axios.get(`/${username}`, {
        headers: {
          'Access-Control-Allow-Origin': '*',
        },
      })
      this.userInfo.username = data.person.name
      this.userInfo.job = data.person.professionalHeadline
      this.userInfo.description = data.person.summaryOfBio
      this.userInfo.picture = data.person.pictureThumbnail
      this.userInfo.verified = data.person.verified
      this.getEachStrenght(data.strengths)
    },
    getEachStrenght(strenghts) {
      const finalSkills = strenghts.map((skill) => ({
        name: skill.name,
        proficiency: skill.proficiency,
      }))

      finalSkills.forEach((skill) => {
        if (skill.proficiency === 'novice') {
          this.novice.push(skill)
        }

        if (skill.proficiency === 'proficient') {
          this.proficent.push(skill)
        }

        if (skill.proficiency === 'expert') {
          this.expert.push(skill)
        }

        if (skill.proficiency === 'master') {
          this.master.push(skill)
        }
      })
    },
    show() {
      this.active = !this.active
    },
    getSearchUser(value) {
      this.searchInput = value
      this.$fetch()
    },
  },
}
</script>

<style >
.container {
  width: 100%;
}

.cover-image-container {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-top: 2.5rem;
  margin-bottom: 1rem;
}

.user-name h1 {
  font-size: 20px;
  text-align: center;
  font-weight: bold;
  margin-bottom: 1rem;
}

.user-name {
  text-align: center;
  padding: 0 1rem;
}

.user-description {
  margin-top: 0.7rem;
  margin-bottom: 0.7rem;
}

.user-job {
  margin-top: 0.7rem;
  color: gray;
}

.info-container {
  max-width: 1440px;
  margin: 0 auto;
  padding: 0 1rem;
}

.info-title {
  margin-top: 1rem;
  margin-bottom: 1rem;
  color: #f5f5f5c7;
}

.master {
  grid-area: master-grid;
}
.expert {
  grid-area: expert-grid;
}
.proficent {
  grid-area: proficent-grid;
}
.novice {
  grid-area: novice-grid;
}

.info-container-grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 1rem;
  grid-template-areas:
    'master-grid'
    'expert-grid'
    'proficent-grid'
    'novice-grid';
}

.info {
  display: flex;
  flex-direction: column;
  margin: 1rem 0;
}

.info p {
  color: whitesmoke;
}

.info img {
  margin-right: 0.5rem;
  width: 30px;
  height: 30px;
}

.info-img {
  display: flex;
  /* justify-content: center; */
  align-items: center;
}

.skills {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

@media (min-width: 500px) {
  .info-container-grid {
    grid-template-columns: repeat(2, 1fr);
    grid-template-areas:
      'master-grid expert-grid'
      'proficent-grid novice-grid';
  }
}

@media (min-width: 768px) {
  .info-container-grid {
    grid-template-columns: repeat(4, 1fr);
    grid-template-areas: 'master-grid expert-grid proficent-grid novice-grid';
  }
}
</style>

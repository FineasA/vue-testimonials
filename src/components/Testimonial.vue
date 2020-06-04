<template>
  <div
    class="testimonial-container"
    :style="{background: rgbValues[userSelected], boxShadow: rgbBoxShadowValues[userSelected]}"
  >
    <font-awesome-icon
      :icon="['fas', 'quote-left']"
      size="3x"
      :style="{color: 'rgba(0, 0, 0, 0.15)'}"
    ></font-awesome-icon>
    <p class="text">{{testimonialData[userSelected].text}}</p>
    <strong
      class="name"
    >{{testimonialData[userSelected].name.first + ' ' + testimonialData[userSelected].name.last}}</strong>
    <div class="authors-container">
      <div class="author">
        <img @click="changeUserDisplayed(0)" :src="testimonialData[0].picture.medium" alt />
      </div>
      <div class="author">
        <img @click="changeUserDisplayed(1)" :src="testimonialData[1].picture.medium" alt />
      </div>
      <div class="author">
        <img @click="changeUserDisplayed(2)" :src="testimonialData[2].picture.medium" alt />
      </div>
      <div class="author">
        <img @click="changeUserDisplayed(3)" :src="testimonialData[3].picture.medium" alt />
      </div>
      <div class="author">
        <img @click="changeUserDisplayed(4)" :src="testimonialData[4].picture.medium" alt />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      testimonialData: [
        {
          name: {
            first: "",
            last: ""
          },
          picture: {
            medium: ""
          }
        },

        {
          name: {
            first: "",
            last: ""
          },
          picture: {
            medium: ""
          }
        },
        {
          name: {
            first: "",
            last: ""
          },
          picture: {
            medium: ""
          }
        },
        {
          name: {
            first: "",
            last: ""
          },
          picture: {
            medium: ""
          }
        },
        {
          name: {
            first: "",
            last: ""
          },
          picture: {
            medium: ""
          }
        }
      ],
      currentUserDisplayed: {
        name: {
          first: "",
          second: ""
        }
      },
      userSelected: 0,
      customTestimonialText: [
        "Fineas is a highly devoted developer who took way too much time on this project. However he learned many new concepts that helped him organize data.",
        "At first I was sketpical whether or not Fineas was a great addition to our team of front-end web developers, but that quickly changed when I witnessed first hand how commited he was to making sure all the little details were worked on.",
        "People seem to think that you need some sort of high intelligence to understand how to program, Fineas showed me otherwise. He showed that all it takes is persistence and patience. Persistence to get through the challenges of when things don't go as planned, and patience to take a step back and think for a moment of what is currently going wrong.",
        "His ability to adapt to new ideas and concepts makes him a great addition to any team. You can put him in charge of anything, and even if he has not had experience in the matter, he will figure out how to solve the problem.",
        "He's dope."
      ],
      rgbValues: [
        "rgba(235, 59, 90)",
        "rgb(250, 130, 49)",
        "rgb(75, 123, 236)",
        "rgb(165, 94, 234)",
        "rgb(32, 191, 107)"
      ],
      rgbBoxShadowValues: [
        "rgba(235, 59, 90, 0.9) 0px 35px 10px -20px",
        "rgba(250, 130, 49, 0.9) 0px 35px 10px -20px",
        "rgba(75, 123, 236, 0.9) 0px 35px 10px -20px",
        "rgba(165, 94, 234, 0.9) 0px 35px 10px -20px",
        "rgba(32, 191, 107, 0.9) 0px 35px 10px -20px"
      ]
    };
  },
  methods: {
    changeUserDisplayed(index) {
      this.userSelected = index;
    },

    async getUserData() {
      await this.$http
        .get(`https://randomuser.me/api/?inc=name,picture&results=5&nat=us`)
        .then(response => {
          this.testimonialData = response.data.results;

          for (let i = 0; i < this.testimonialData.length; i++) {
            this.testimonialData[i].text = this.customTestimonialText[i];
          }
        });
      console.log(this.testimonialData[0]);
      console.log(this.testimonialData);
    }
  },
  created() {
    this.getUserData();
  }
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Ubuntu&display=swap");

.author {
  margin: 30px 30px 0;
  cursor: pointer;
}

.author img {
  transition: all 0.3s ease-in;
  border-radius: 50%;
  width: 50px;
  height: 50px;
}
.authors-container {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  justify-content: center;
}
.name {
  align-self: flex-end;
  font-weight: bold;
  letter-spacing: 2px;
  text-transform: uppercase;
}
.text {
  color: white;
  font-family: "Ubuntu", sans-serif;
  line-height: 30px;
  margin: 40px 0 20px;
  min-height: 150px;
  max-width: 600px;
  text-align: justify;
  word-spacing: 5px;
}
.testimonial-container {
  transition: all 0.3s ease-in;
  margin: 0 auto !important;
  margin-top: 25% !important;
  height: 55vh;
  max-width: 55vw !important;
  margin: 20px;
  padding: 70px 50px 50px;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.quote-custom {
  color: rgba(0, 0, 0, 0.15);
  font-size: 50px;
}
</style>
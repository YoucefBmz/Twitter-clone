<template>
  <div id="app" class="flex container h-screen w-full">
    <!-- side bar -->
    <div
      class="lg:w-1/5 border-r border-lighter px-2 lg:px-8 py-2 flex flex-col justify-between"
    >
      <div>
        <button
          class="h-12 w-12 hover:bg-lightblue text-3xl text-blue outline-white rounded-full focus:outline-none"
        >
          <i class="fa fa-twitter rounded" aria-hidden="true"></i>
        </button>
        <button
          v-for="tab in tabs"
          :key="tab.id"
          @click="id = tab.id"
          :class="`flex items-center py-2 px-4 hover:bg-lightblue rounded-full mr-auto mb-1 focus:outline-none hover:text-blue ${
            id === tab.id ? 'text-blue' : ''
          }`"
        >
          <i :class="`${tab.icon} text-2xl mr-4 text-left`"></i>
          <p class="text-lg font-semibold text-left hidden lg:block">
            {{ tab.title }}
          </p>
        </button>
        <button
          class="text-white bg-blue rounded-full font-semibold w-12 h-12 lg:h-auto lg:w-full p-3 hover:bg-darkblue focus:outline-none"
        >
          <p class="hidden lg:block">Tweet</p>
          <i class="fas fa-plus lg:hidden"></i>
        </button>
      </div>
      <div @click="dropDown = !dropDown" class="relative lg:w-full">
        <button
          class="flex items-center w-full focus:outline-none hover:bg-lightest rounded-full p-2"
        >
          <img
            src="profil.jpg"
            alt="img"
            class="rounded-full w-10 h-10 border border-lightblue"
          />
          <div class="ml-4 hidden lg:block">
            <p class="text-sm font-bold leading-tight">youcf Bmz</p>
            <p class="text-sm leading-tight">@YoucefBmz</p>
          </div>
          <i class="fas fa-angle-down ml-auto text-lg hidden lg:block"></i>
        </button>
        <div
          v-if="dropDown"
          class="absolute bottom-0 right-0 w-64 rounded-lg shadow-md border-lightest p-2 focus:outline-none bg-white mb-16"
        >
          <button
            class="flex items-center w-full focus:outline-none hover:bg-lightest rounded-full p-2"
          >
            <img
              src="profil.jpg"
              alt="img"
              class="rounded-full w-10 h-10 border border-lightblue"
            />
            <div class="ml-4">
              <p class="text-sm font-bold leading-tight">youcf Bmz</p>
              <p class="text-sm leading-tight">@YoucefBmz</p>
            </div>
            <i class="fas fa-check ml-auto text-blue"></i>
          </button>
          <button
            class="w-full text-left hover:bg-lightest border-t border-lighter p-3 text-sm"
          >
            Add an existing account
          </button>
          <button
            class="w-full text-left hover:bg-lightest border-t border-lighter p-3 text-sm"
          >
            Log out @YoucefBmz
          </button>
        </div>
      </div>
    </div>
    <!-- tweets -->
    <div class="w-1/2 h-full overflow-y-scroll">
      <div
        class="px-5 py-3 borber-b border-lighter flex items-center justify-between"
      >
        <h1 class="text-xl font-bold">Home</h1>
        <i class="far fa-star text-xl text-blue"></i>
      </div>
      <div class="px-5 py-3 border-b-8 border-lighter flex">
        <div class="">
          <img
            src="profil.jpg"
            alt=""
            class="w-12 h-12 object-cover rounded-full border border-lighter"
          />
        </div>
        <form
          v-on:submit.prevent="addNewTweet"
          action=""
          class="w-full px-4 relative"
        >
          <textarea
            v-model="tweet"
            class="w-full focus:outline-none p-3 bg-lightest"
            placeholder="what's up"
          ></textarea>
          <div class="flex items-center">
            <i class="text-lg text-blue mr-4 far fa-image"></i>
            <i class="text-lg text-blue mr-4 fas fa-film"></i>
            <i class="text-lg text-blue mr-4 far fa-chart-bar"></i>
            <i class="text-lg text-blue mr-4 far fa-smile"></i>
          </div>
          <button
            class="h-8 mt-3 px-4 text-white font-semibold bg-blue hover:bg-darkblue focus:outline-none rounded-full absolute bottom-0 right-0"
          >
            Tweet
          </button>
        </form>
      </div>
      <div
        v-for="tweet in tweets"
        :key="tweet.contet"
        class="w-full p-4 border-b hover:bg-lighter flex"
      >
        <div class="flex-none mr-4">
          <img src="profil.jpg" class="h-12 w-12 rounded-full flex-none" />
        </div>
        <div class="w-full">
          <div class="flex items-center w-full">
            <p class="font-semibold">Youcef Bmz</p>
            <p class="text-sm text-dark ml-2">@YoucefBmz</p>
            <p class="text-sm text-dark ml-2">1 sec</p>
            <i class="fas fa-angle-down text-dark ml-auto"></i>
          </div>
          <p class="py-2">
            {{ tweet.content }}
          </p>
          <div class="flex items-center justify-between w-full">
            <div class="flex items-center text-sm text-dark">
              <i class="far fa-comment mr-3"></i>
              <p>0</p>
            </div>
            <div class="flex items-center text-sm text-dark">
              <i class="fas fa-retweet mr-3"></i>
              <p>0</p>
            </div>
            <div class="flex items-center text-sm text-dark">
              <i class="fas fa-heart mr-3"></i>
              <p>1</p>
            </div>
            <div class="flex items-center text-sm text-dark">
              <i class="fas fa-share-square mr-3"></i>
            </div>
          </div>
        </div>
      </div>
      <div
        v-for="follow in following"
        :key="follow.handle"
        class="w-full p-4 border-b hover:bg-lighter flex"
      >
        <div class="flex-none mr-4">
          <img
            src="profil.jpg"
            class="w-12 h-12 rounded-full flex-none"
            alt=""
          />
        </div>
        <div class="w-full">
          <div class="flex items-center w-full">
            <p class="font-semibold">{{ follow.name }}</p>
            <p class="text-sm text-dark ml-2">{{ follow.handle }}</p>
            <i class="fas fa-angle-down text-dark ml-auto"></i>
          </div>
          <p class="py-2">
            {{ follow.tweet }}
          </p>
          <div class="flex items-center justify-between w-full">
            <div class="flex items-center text-sm text-dark">
              <i class="far fa-comment mr-3"></i>
              <p class="">{{ follow.comments }}</p>
            </div>
            <div class="flex items-center text-sm text-dark">
              <i class="fas fa-retweet mr-3"></i>
              <p class="">{{ follow.retweets }}</p>
            </div>
            <div class="flex items-center text-sm text-dark">
              <i class="fas fa-heart mr-3"></i>
              <p class="">{{ follow.like }}</p>
            </div>
            <div class="flex items-center text-sm text-dark">
              <i class="fas fa-share-square mr-3"></i>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- -->
    <div
      class="md:block hidden relative w-1/3 h-full border-l border-lighter py-2 px-6 overflow-y-scroll"
    >
      <input
        type="text"
        class="rounded-full w-full p-2 bg-lighter text-sm pl-12 focus:outline-none"
        placeholder="search Twitter"
      />
      <i
        class="fas fa-search absolute left-0 top-0 mt-4 ml-12 text-sm text-light"
      ></i>
      <div class="w-full rounded-lg bg-lightest">
        <div class="flex items-center justify-between p-3">
          <p class="text-lg font-bold">Trends for you</p>
          <i class="fas fa-cog text-lg text-blue"></i>
        </div>
        <button
          v-for="trend in trending"
          :key="trend.title"
          class="w-full flex justify-between hover:bg-lighter p-3"
        >
          <p class="text-sm text-left leading-tight focus:outline-none">
            {{ trend.top }}
          </p>
          <p class="font-bold text-left leading-tight">{{ trend.title }}</p>
          <p class="text-left leading-tight text-dark">{{ trend.bottom }}</p>
          <i class="fas fa-angle-down text-lg text-dark"></i>
        </button>
        <button
          class="p-3 w-full hover:bg-lighter text-blue border-tborder-lighter text-center focus:outline-none"
        >
          Show More
        </button>
      </div>

      <div class="w-full rounded-lg bg-lightest">
        <div class="flex items-center justify-between p-3">
          <p class="text-lg font-bold">Who to follow</p>
        </div>
        <button
          v-for="friend in friends"
          :key="friend.handle"
          class="w-full flex items-center hover:bg-lighter p-3 border border-lighter focus:outline-none"
        >
          <img
            src="profil.jpg"
            alt="img"
            class="rounded-full w-12 h-12 border border-lightblue"
          />
          <div class="ml-4 hidden lg:block">
            <p class="text-sm font-bold leading-tight">
              {{ friend.name }}
            </p>
            <p class="text-sm leading-tight">
              {{ friend.handle }}
            </p>
          </div>
          <p
            class="ml-auto text-sm text-blue py-1 px-4 rounded-full border-2 border-blue"
          >
            Follow
          </p>
        </button>
        <button
          class="p-3 w-full hover:bg-lighter text-blue border-tborder-lighter text-center focus:outline-none"
        >
          Show More
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import NavBar from "./components/NavBar.vue";
export default {
  name: "App",
  components: { NavBar },
  data() {
    return {
      tabs: [
        { icon: "fas fa-home", title: "Home", id: "home" },
        { icon: "fas fa-hashtag", title: "Explore", id: "explore" },
        { icon: "far fa-bell", title: "Notifications", id: "notifications" },
        { icon: "far fa-envelope", title: "Messages", id: "messages" },
        { icon: "far fa-bookmark", title: "Bookmarks", id: "bookmarks" },
        { icon: "fas fa-clipboard-list", title: "Lists", id: "lists" },
        { icon: "far fa-user", title: "Profile", id: "profile" },
        { icon: "fas fa-ellipsis-h", title: "More", id: "more" },
      ],
      id: "home", //
      dropDown: false,
      trending: [
        {
          top: "Trending in TX",
          title: "Gigi",
          bottom: "Trending with: Rip Gigi",
        },
        { top: "Music", title: "We Won", bottom: "135K Tweets" },
        { top: "Pop", title: "Blue Ivy", bottom: "40k tweets" },
        { top: "Trending in US", title: "Denim Day", bottom: "40k tweets" },
        { top: "Trending", title: "When Beyonce", bottom: "25.4k tweets" },
      ],

      friends: [
        { src: "elon.jpg", name: "Elon Musk", handle: "@teslaBoy" },
        { src: "monk.jpg", name: "Adrian Monk", handle: "@detective:)" },
        { src: "kevin.jpg", name: "Kevin Hart", handle: "@miniRock" },
      ],
      following: [
        {
          src: "elon.jpg",
          name: "Elon Musk",
          handle: "@teslaBoy",
          time: "20 min",
          tweet: "Should I just quarantine on mars??",
          comments: "1,000",
          retweets: "550",
          like: "1,000,003",
        },
        {
          src: "kevin.jpg",
          name: "Kevin Hart",
          handle: "@miniRock",
          time: "55 min",
          tweet: "Should me and the rock do another sub-par movie together????",
          comments: "2,030",
          retweets: "50",
          like: "20,003",
        },
        {
          src: "elon.jpg",
          name: "Elon Musk",
          handle: "@teslaBoy",
          time: "1.4 hr",
          tweet: "Haha just made a flame thrower. Shld I sell them?",
          comments: "100,000",
          retweets: "1,000,002",
          like: "5,000,003",
        },
        {
          src: "elon.jpg",
          name: "Elon Musk",
          handle: "@teslaBoy",
          time: "1.4 hr",
          tweet: "Just did something crazyyyyyyy",
          comments: "100,500",
          retweets: "1,000,032",
          like: "5,000,103",
        },
      ],
      tweets: [{ content: "it's cool out side!!" }],
      tweet: "",
    };
  },
  methods: {
    addNewTweet() {
      let newTweet = {
        content: this.tweet,
      };
      this.tweets.unshift(newTweet);
      this.tweet = "";
    },
  },
};
</script>

<style>
.youcef {
  outline: none;
}
</style>

<template>
  <div>
    <div class="input-wrapper">
      <div class="input-container">
        <img :src="images.linkImage" alt="" class="image" />
        <input
          type="text"
          placeholder="Enter your link here..."
          v-model="text"
        />
      </div>
      <div class="btn-wrapper">
        <div class="go-container" @click="handleTextChange">
          <i class="fa-solid fa-circle-play"></i>
        </div>
        <div class="reload-container" @click="clearUrl">
          <img :src="images.reload" alt="" class="image" />
        </div>
      </div>
    </div>

    <div class="result-contianer">
      <input
        type="text"
        :value="result"
        :placeholder="loading ? 'loading...' : 'Result'"
      />
      <div class="copy-text" @click="copyResult">
        <img :src="images.copyLinkImage" alt="" class="copy_image" />
        <div class="copy-link-text">Copy Link</div>
      </div>
    </div>
  </div>
</template>

<script>
import linkImage from "../assets/carbon_link.png";
import reload from "../assets/reload.png";
import copyLinkImage from "../assets/copyLink.png";
import axios from "axios";

export default {
  data() {
    return {
      text: "",
      images: {
        linkImage: linkImage,
        reload,
        copyLinkImage,
      },
      loading: false,
      result: "",
    };
  },

  methods: {
    checkIfUrlIsValid() {
      const urlPattern = /^https?:\/\//i; // Regular expression to check if URL starts with "https://" or "http://"
      return !urlPattern.test(this.text); // Return true if the URL doesn't match the pattern (i.e., it's not valid)
    },

    handleTextChange() {
      if (!this.text) {
        alert("Please enter a url!");
      } else if (this.checkIfUrlIsValid()) {
        alert("Enter a valid URL starting with 'https://' or 'http://'");
      } else {
        this.handleFetchShortenedUrl();
      }
    },

    clearUrl() {
      this.text = "";
      this.result = "";
    },

    async handleFetchShortenedUrl() {
      const encodedParams = new URLSearchParams();
      encodedParams.set("url", this.text);
      const options = {
        method: "POST",
        url: "https://url-shortener-service.p.rapidapi.com/shorten",
        headers: {
          "content-type": "application/x-www-form-urlencoded",
          "X-RapidAPI-Key":
            "a8e7b07c4bmsh181d58aead32579p15de63jsnfaffb3adfeb9",
          "X-RapidAPI-Host": "url-shortener-service.p.rapidapi.com",
        },
        data: encodedParams,
      };
      try {
        this.loading = true;
        const response = await axios.request(options);
        this.result = response.data.result_url;
      } catch (error) {
        console.log(error);
      } finally {
        this.loading = false;
      }
    },

    copyResult() {
      if (this.result !== "") {
        navigator.clipboard
          .writeText(this.result)
          .then(() => {
            alert("Link copied");
            // Optionally, you can show a success message or perform any other action here
          })
          .catch((err) => {
            alert("Could not copy text: ", err);
            console.log(err);
            // Optionally, you can show an error message or perform any other action here
          });
      }
    },
  },
};
</script>

<style scoped>
.image {
  height: 20px;
}

.input-wrapper {
  display: flex;
  align-items: center;
  gap: 40px;
}

.input-container {
  display: flex;
  align-items: center;
  padding: 0 10px;
  gap: 10px;
  background: #1c1e20;
  width: 400px;
  border-radius: 8px;
}

.input-container,
.reload-container {
  border: 1px solid #ffffff;
}

.reload-container {
  width: 40px;
  height: 40px;
  display: grid;
  place-items: center;
  padding: 0 10px;
  cursor: pointer;
  background: #1c1e20;
  border-radius: 8px;
}
.go-container {
  width: 40px;
  height: 40px;
  display: grid;
  place-items: center;
  cursor: pointer;
  background: #1c1e20;
  border-radius: 8px;
  border: 1px solid #ffffff;
}

.input-container input {
  background-color: transparent;
  border: 0;
  outline: none;
  color: #ffffff;
  height: 40px;
  width: auto;
}
.result-contianer {
  display: flex;
  align-items: center;
  margin-top: 20px;
  gap: 10px;
}
.result-contianer input {
  background-color: #1c1e20;
  border: 1px solid #ffffff;
  outline: none;
  color: #ffffff;
  height: 40px;
  width: auto;
  border-radius: 8px;
  width: 350px;
  padding: 0 10px;
}

.copy-text {
  display: flex;
  background-color: #1c1e20;
  border: 1px solid #ffffff;
  height: 40px;
  border-radius: 8px;
  width: 120px;
  justify-content: center;
  align-items: center;
  gap: 10px;
  cursor: pointer;
}
.copy-link-text {
  font-size: 12px !important;
  font-weight: 400 !important;
  font-family: "Roboto", sans-serif;
}

.copy_image {
  height: 20px;
  width: 20px;
}

.btn-wrapper {
  display: flex;
  gap: 10px;
}

@media (max-width: 700px) {
  .input-container {
    width: 100%;
  }
  .result-contianer input {
    width: 100%;
  }

  .copy-text {
    width: 170px;
  }
}
</style>

<template>
     
<div class="article-feed-container">
  
    <div class="article-feed">
      <h2>Write Column</h2>
      <transition name="fade"><div v-if="isLoading" class="loading-mask"><div class="loading-pulse"><p>Loading...</p></div></div></transition>
      <ul>
        <li v-for="article in articles" :key="article.id">
          <div @click="toggleArticle(article.id)" class="accordion-item">
            <h3 >{{ article.title }}</h3>
            <div class="pubdate">{{ article.pubDate }}</div>            
            <div v-if="expandedArticles[article.id]">{{ article.content.substring(0, 85) }}...
            <p></p><button class="readmore" href="#" @click.prevent="console.log(article.id)">Read More</button>  
            
            </div>
            
            <div class="accordion-content" :class="{ show: !expandedArticles[article.id] }">
              <div  class="content-box" v-if="!expandedArticles[article.id]">
                {{ article.content }}
              
              
                <div class="close-button-container"><button class="close" href="#" @click.prevent="console.log(article.id)">Close</button>    </div>
              
              </div>
              
              <div v-else>
                <!-- Does this even show? -->
                {{ article.content }}...
                
                
              
              
              </div>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </div>
  </template>
  


  <style>
/* General scrollbar styling */
::-webkit-scrollbar {
  width: 10px; /* Adjust width as needed */
}

::-webkit-scrollbar-track {
  background: #f1f1f17a; /* Adjust track color as needed */
  border-radius: 5px; /* Add rounded corners to the track */
}

::-webkit-scrollbar-thumb {
  background: #afafaf60; /* Adjust thumb color as needed */
  border-radius: 5px; /* Add rounded corners to the thumb */
}

::-webkit-scrollbar-thumb:hover {
  background: #555; /* Adjust hover color as needed */
}

/* Fade transition for loading mask */
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}

/* Pulse animation for loading indicator */
@keyframes pulse {
  0% { transform: scale(0.95); opacity: 0.3; }
  50% { transform: scale(1); opacity: 1; }
  100% { transform: scale(0.95); opacity: 0.5; }
}

.article-feed-container
{
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 3px 3px 6px rgba(2, 2, 2, 0.5);
  align-items: center;
  padding: 1px;
  justify-content: center;
  background: radial-gradient(circle, rgba(333, 333, 333, 0.295), rgba(777, 777, 777, 0.295) )

}
.loading-mask {
  text-align: center;
  display: flex;
  height: 30px;
  width: 100%;
  background-color: rgba(87, 87, 87, 0.226); /* Adjust opacity as needed */
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 100; /* Ensure it's on top */
  border-radius: 10px;
}
.loading-pulse {
  display: flex;
  width: 100%;
  justify-content: center;
  align-items: center;
  text-align: center;
  height: 100%;
  border-radius: 10px;
  background-color: rgba(36, 36, 36, 0.360); /* Adjust color and opacity as needed */
  animation: pulse 440ms ease-in-out infinite; 
}
  

  .article-feed {
    background: linear-gradient(to bottom, rgba(0, 0, 0, 0.185), rgba(122, 122, 122, 0));
    border: 1px solid rgba(168, 168, 168, 0.411);
    border-radius: 10px;
    padding: 20px;
    color: white;
    filter: invert(0);
    width: 400px;
    overflow: auto;
    scroll-behavior: smooth;
    scrollbar-width: thin;
    height: calc(100vh - 120px);
    
  }
  
  .article-feed ul {
    list-style-type: none;
    padding: 0;
   
  }
  
  .article-feed li {
    background: rgba(255, 255, 255, 0.26);
    border-radius: 5px;
    padding: 20px;
    margin-bottom: 10px;
    box-shadow: 3px 3px 5px rgba(0, 0, 0, 0.5);
    cursor: pointer;
    color: black;
    filter: invert(0);
  }
  
  .article-feed a {
    color: #333;
    text-decoration: none;
    display: block;
    
  }
  
  .article-feed a:hover {
    text-decoration: underline;
    color: #007bff;
    
  }
  
  .accordion-content {
    display: none;
    margin: 20px;
    
  }
  
  .accordion-content.show {
    display: block;
    
  }
  .content-box
  {
    text-align: justify;
   
  }
  .pubdate
  {
    font-size: 8pt;
    /* background: repeating-radial-gradient(circle, #3333331e, #b6b6b660, #6161613b); */
    border-radius: 5px;
  }
  .readmore:hover
  {
    background: repeating-radial-gradient(circle, #e2e2e280, #b6b6b686, #85848479);
  }
  .readmore
  {
    font-size: 8pt;
    background: repeating-radial-gradient(circle, #ffffff49, #b6b6b648, #85848400);
    border-radius: 5px;
    color: rgb(66, 66, 66);
    border: 2px solid #3f3f3f55;
    padding-top: 1px;
    height: 25px;
    padding-bottom: 1px;
  }
  .close:hover
  {
    background: repeating-radial-gradient(circle, #ffffff80, #b6b6b686, #85848479);
  }
  .close
  {
    padding-top: 1px;
    padding-bottom: 1px;
    border: 1px solid #333;
    color: rgb(66, 66, 66);
    font-size: 8pt;
    background: repeating-radial-gradient(circle, #ffffff36, #c7c6c623, #85848400);
    border-radius: 5px;
    height: 25px;
  }
  .close-button-container
  {
    display: flex;
    justify-content: center;
    align-items: center;
  }
  </style>



  <script>
  export default {
    data() {
      return {
        isLoading: true,
        articles: [
          {
            id: 1,
            title: 'Blog Entry 1',
            pubDate: '2024 Nov 15',
            content: 'Have you ever decided to write a blog? Me neither. I only wrote this so I would have a blog on my site.'
            + ' So I decided to write this lorem ipsum dolor whatever I dunno the rest.'

          },
          {
            id: 2,
            title: 'Article 2',
            pubDate: '2024 Nov 15',
            content: 'This is the content of Article 2. It is another long piece of text that will be truncated.'
          },
          {
            id: 3,
            title: 'Article 3',
            pubDate: '2024 Nov 15',
            content: 'This is the content of Article 3. It is yet another long piece of text that will be truncated.'
          }
        ],
        expandedArticles: {}
      };
      
    },
    created() {
      //this.fetchArticles();
      this.loadMockedData(); 
    },
    methods: {
      loadMockedData() {
      this.articles.forEach(article => {
          this.expandedArticles[article.id] = true; 
        });
        setTimeout(() => {
        this.isLoading = false; 
        }, 1000); 
      },
      async fetchArticles() {
        try {
          const response = await fetch('https://www.google.com/api/v1/blog/latest');
          if (!response.ok) {
            throw new Error(`HTTP error! status: ${response.status}`);
          }
          this.articles = await response.json();
        } catch (error) {
          console.error('Error fetching articles:', error);
        } finally {
          this.isLoading = false;
        }
      },
 
      toggleArticle(id) {
        console.log("toggleArticle(" + id + "): got here 1");
        console.log(this.expandedArticles[id]);
        this.expandedArticles[id] = !this.expandedArticles[id];
        console.log(this.expandedArticles[id]);
      }
    }
  };
  </script>
  @media (max-width: 450px) {
  .article-feed {
    width: calc(100vw - 20px);
    height: auto;
  }
}
  
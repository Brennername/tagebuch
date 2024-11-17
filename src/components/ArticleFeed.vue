<template>
    <div class="article-feed-container">
    <div class="article-feed">
      <h2>Latest Articles</h2>
      <ul>
        <li v-for="article in articles" :key="article.id">
          <div @click="toggleArticle(article.id)" class="accordion-item">
            <h3 >{{ article.title }}</h3>
            <div class="pubdate">{{ article.pubDate }}</div>            
            <div v-if="expandedArticles[article.id]">{{ article.content.substring(0, 20) }}...
            <p></p><button class="readmore" href="#" @click.prevent="console.log(article.id)">Read More</button>  
            
            </div>
            
            <div class="accordion-content" :class="{ show: !expandedArticles[article.id] }">
              <p  class="content-box" v-if="!expandedArticles[article.id]">
                {{ article.content }}
              
              
                <p class="close-button-container"><button class="close" href="#" @click.prevent="console.log(article.id)">Close</button>    </p>
              
              </p>
              
              <p v-else>
                {{ article.content.substring(0, 5) }}...
                
                
              
              
              </p>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        articles: [
          {
            id: 1,
            title: 'Blog Entry 1',
            pubDate: '2024 Nov 15',
            content: 'This is the content of Article 1. It is a long piece of text that will be truncated.'
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
      this.articles.forEach(article => {
    this.expandedArticles[article.id] = true; // Initialize to false (collapsed)
    });
    },
    methods: {
      toggleArticle(id) {
        console.log("toggleArticle(" + id + "): got here 1");
        console.log(this.expandedArticles[id]);
        this.expandedArticles[id] = !this.expandedArticles[id];
        console.log(this.expandedArticles[id]);
      }
    }
  };
  </script>
  
  <style>
/* General scrollbar styling */
::-webkit-scrollbar {
  width: 10px; /* Adjust width as needed */
}

::-webkit-scrollbar-track {
  background: #f1f1f1; /* Adjust track color as needed */
  border-radius: 5px; /* Add rounded corners to the track */
}

::-webkit-scrollbar-thumb {
  background: #888; /* Adjust thumb color as needed */
  border-radius: 5px; /* Add rounded corners to the thumb */
}

::-webkit-scrollbar-thumb:hover {
  background: #555; /* Adjust hover color as needed */
}
.article-feed-container
{
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 3px 3px 6px rgba(0, 0, 0, 0.295);
}
  .article-feed {
    background: linear-gradient(to bottom, rgba(0, 0, 0, 0.185), rgba(122, 122, 122, 0));
    border: 1px solid rgba(168, 168, 168, 0.411);
    border-radius: 10px;
    padding: 20px;
    color: white;
    filter: invert(0);
    width: 300px;
    overflow: auto;
    scroll-behavior: smooth;
    scrollbar-width: thin;
    height: 620px;
    
  }
  
  .article-feed ul {
    list-style-type: none;
    padding: 0;
   
  }
  
  .article-feed li {
    background: rgba(255, 255, 255, 0.26);
    border-radius: 5px;
    padding: 10px;
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
    margin-left: 20px;
    
  }
  
  .accordion-content.show {
    display: block;
    
  }
  .content-box
  {
    text-align: left;
   
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
    border: 1px solid #ffffff55;
    padding-top: 1px;
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
  }
  .close-button-container
  {
    display: flex;
    justify-content: center;
    align-items: center;
  }
  </style>
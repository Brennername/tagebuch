<template>
    <div class="article-feed">
      <h2>Latest Articles</h2>
      <ul>
        <li v-for="article in articles" :key="article.id">
          <div @click="toggleArticle(article.id)" class="accordion-item">
            <h3 >{{ article.title }}</h3>
            <div class="accordion-content" :class="{ show: expandedArticles[article.id] }">
              <p v-if="!expandedArticles[article.id]">
                {{ article.content.substring(0, 100) }}...
                <a href="#" @click.prevent="toggleArticle(article.id)">Read More</a>
              </p>
              <p v-else>{{ article.content }}</p>
            </div>
          </div>
        </li>
      </ul>
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
            content: 'This is the content of Article 1. It is a long piece of text that will be truncated.'
          },
          {
            id: 2,
            title: 'Article 2',
            content: 'This is the content of Article 2. It is another long piece of text that will be truncated.'
          },
          {
            id: 3,
            title: 'Article 3',
            content: 'This is the content of Article 3. It is yet another long piece of text that will be truncated.'
          }
        ],
        expandedArticles: {}
      };
    },
    methods: {
      toggleArticle(id) {
        this.expandedArticles[id] = !this.expandedArticles[id];
      }
    }
  };
  </script>
  
  <style>
  body
  {
    color: black;
  }
  .article-feed {
    background: linear-gradient(to bottom, rgba(0, 0, 0, 0.185), rgba(122, 122, 122, 0.2));
    border-radius: 10px;
    padding: 20px;
    color: white;
    /* filter: invert(1); */
    width: 400px;
    
  }
  
  .article-feed ul {
    list-style-type: none;
    padding: 0;
  }
  
  .article-feed li {
    background: rgba(255, 255, 255, 0.5);
    border-radius: 5px;
    padding: 10px;
    margin-bottom: 10px;
    box-shadow: 3px 3px 5px rgba(0, 0, 0, 0.5);
    cursor: pointer;
    color: black;
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
  </style>
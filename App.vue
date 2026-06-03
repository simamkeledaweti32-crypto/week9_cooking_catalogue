<template>
  <div class="container">
    <header>
      <h1>Cooking Masterclass Catalogue</h1>
      <div class="saved-counter">
        Saved: {{ savedCourses.length }}
      </div>
    </header>

    <main class="course-grid">
      <div 
        v-for="course in courses" 
        :key="course.id" 
        class="course-card"
      >
        <h2>{{ course.title }}</h2>
        <p><strong>Chef:</strong> {{ course.chef }}</p>
        <p><strong>Price:</strong> R{{ course.price }}</p>
        <p><strong>Level:</strong> {{ course.level }}</p>
        
        <span v-if="course.soldOut" class="badge sold-out">
          Sold Out
        </span>

        <button 
          @click="saveCourse(course)"
          :disabled="course.soldOut || isSaved(course.id)"
        >
          {{ isSaved(course.id) ? 'Saved ✓' : 'Save Course' }}
        </button>
      </div>
    </main>

    <section v-if="savedCourses.length > 0" class="saved-section">
      <h2>Your Saved Courses</h2>
      <ul>
        <li v-for="course in savedCourses" :key="'saved-' + course.id">
          {{ course.title }} - R{{ course.price }}
        </li>
      </ul>
    </section>
  </div>
</template>

<script>
export default {
  data() {
    return {
      courses: [
        { id: 1, title: 'Italian Pasta Basics', chef: 'Chef Maria', price: 450, level: 'Beginner', soldOut: false },
        { id: 2, title: 'Sushi Masterclass', chef: 'Chef Kenji', price: 650, level: 'Advanced', soldOut: true },
        { id: 3, title: 'French Pastry', chef: 'Chef Pierre', price: 550, level: 'Intermediate', soldOut: false },
        { id: 4, title: 'BBQ & Grilling', chef: 'Chef Thabo', price: 400, level: 'Beginner', soldOut: false },
        { id: 5, title: 'Vegan Cooking', chef: 'Chef Lisa', price: 500, level: 'Intermediate', soldOut: false },
        { id: 6, title: 'Chocolate Desserts', chef: 'Chef Anna', price: 600, level: 'Advanced', soldOut: true }
      ],
      savedCourses: []
    }
  },
  methods: {
    saveCourse(course) {
      if (!this.isSaved(course.id) && !course.soldOut) {
        this.savedCourses.push(course)
      }
    },
    isSaved(id) {
      return this.savedCourses.some(c => c.id === id)
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: Arial, sans-serif;
  background: #f5f5f5;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: #ff6b35;
  color: white;
  padding: 20px;
  border-radius: 8px;
  margin-bottom: 30px;
}

.saved-counter {
  font-size: 18px;
  font-weight: bold;
}

.course-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 20px;
  margin-bottom: 40px;
}

.course-card {
  background: white;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
}

.course-card h2 {
  color: #333;
  margin-bottom: 10px;
  font-size: 18px;
}

.course-card p {
  margin: 5px 0;
  color: #666;
}

.badge.sold-out {
  display: inline-block;
  background: #dc3545;
  color: white;
  padding: 5px 10px;
  border-radius: 4px;
  font-size: 12px;
  margin: 10px 0;
}

button {
  width: 100%;
  padding: 10px;
  margin-top: 10px;
  background: #28a745;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
}

button:disabled {
  background: #ccc;
  cursor: not-allowed;
}

.saved-section {
  background: white;
  padding: 20px;
  border-radius: 8px;
}

.saved-section h2 {
  margin-bottom: 15px;
}

.saved-section li {
  padding: 8px 0;
  border-bottom: 1px solid #eee;
}

@media (max-width: 768px) {
  header {
    flex-direction: column;
    gap: 10px;
  }
  
  .course-grid {
    grid-template-columns: 1fr;
  }
}
</style>

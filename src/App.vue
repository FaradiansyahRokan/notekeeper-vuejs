<script setup>
import { ref } from 'vue';

const showModal = ref(false);
const newMemo = ref("");
const memos = ref([]);

const closeModal = () => {
  showModal.value = false;
};


function saveMemo(){
  memos.value.push({
    id: Date.now(),
    content: newMemo.value,
    date: new Date().toLocaleDateString()
  });

  newMemo.value = "";
  showModal.value = false;
}
</script>

<template>
  <main>
    <div class="container">
      <header>
        <h1>Notes.</h1>
        <button @click="showModal = true" class="add-btn">+</button>
      </header>
      
      <div v-if="memos.length === 0" class="empty-state">
        <p>Belum Ada Notes. , Bikin Baru Untuk Menampilkan</p>
      </div>
      
      <div v-else class="card-container">
        <div v-for="memo in memos" class="card">
          <p class="">{{ memo.content }}</p>
          <p class="date">{{ memo.date }}</p>
        </div>
      </div>
    </div>
  </main>
  
  <div v-if="showModal" class="modal-overlay">
    <div class="modal">
      <header>
        <h2>Bikin Notes Baruwww</h2>
        <span @click="closeModal" class="close-btn">&times;</span>
      </header>
      <textarea v-model="newMemo" placeholder="Tulis Nites Baru Di Siniiii"></textarea>
      <div class="modal-actions">
        <button @click="saveMemo" class="save-btn">Save</button>
        <button @click="closeModal" class="cancel-btn">Cancel</button>
      </div>
    </div>
  </div>
</template>

<style scoped>
/*
  =================
  Base & Container
  =================
*/
main {
  background: #f0f2f5;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: flex-start;
  padding: 40px 20px;
  font-family: 'Inter', sans-serif;
  color: #333;
}

.container {
  background: #ffffff;
  width: 100%;
  max-width: 700px;
  padding: 30px;
  border-radius: 16px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.08);
}

/*
  =================
  Header
  =================
*/
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 30px;
}

header h1 {
  font-size: 2.2rem;
  font-weight: 700;
  color: #1e1e1e;
}

.add-btn {
  background: linear-gradient(135deg, #4f9efc, #2563eb);
  color: white;
  border: none;
  padding: 10px 18px;
  font-size: 1.5rem;
  border-radius: 10px;
  cursor: pointer;
  transition: all 0.2s ease;
  box-shadow: 0 4px 10px rgba(37, 99, 235, 0.3);
}

.add-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 15px rgba(37, 99, 235, 0.4);
}

.add-btn:active {
  transform: scale(0.95);
  box-shadow: 0 2px 5px rgba(37, 99, 235, 0.3);
}

/*
  =================
  Cards
  =================
*/
.card-container {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 25px;
}

.card {
  background: #ffffff;
  padding: 20px;
  border-radius: 12px;
  color: #555;
  font-size: 1rem;
  min-height: 140px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  border: 1px solid #e0e0e0;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
  transition: transform 0.2s ease, box-shadow 0.2s ease;
  word-wrap: break-word;
  overflow-wrap: break-word;
}

.card:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.1);
}

.card p {
  margin: 0;
  line-height: 1.6;
}

.card .date {
  font-size: 0.9rem;
  color: #999;
  margin-top: 15px;
  align-self: flex-end;
}

/*
  =================
  Empty State
  =================
*/
.empty-state {
  text-align: center;
  color: #888;
  padding: 60px 20px;
  border: 2px dashed #e0e0e0;
  border-radius: 12px;
  margin-top: 20px;
}

/*
  =================
  Modal
  =================
*/
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
}

.modal {
  background: #ffffff;
  padding: 25px;
  border-radius: 12px;
  width: 450px;
  max-width: 90%;
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);
  animation: fadeIn 0.3s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}

.modal header {
  margin-bottom: 20px;
}

.modal header h2 {
  font-size: 20px;
  font-weight: 600;
  color: #333;
}

.close-btn {
  cursor: pointer;
  font-size: 24px;
  color: #b0b0b0;
  transition: color 0.2s;
}

.close-btn:hover {
  color: #1e1e1e;
}

.modal textarea {
  width: 100%;
  height: 150px;
  /* padding: 12px; */
  border-radius: 8px;
  border: 1px solid #ddd;
  resize: none;
  outline: none;
  font-size: 15px;
  transition: border-color 0.2s;
}

.modal textarea:focus {
  border-color: #2563eb;
  box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.2);
}

.modal-actions {
  display: flex;
  justify-content: flex-end;
  margin-top: 20px;
  gap: 10px;
}

.modal-actions button {
  padding: 10px 20px;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  font-size: 15px;
  font-weight: 500;
  transition: all 0.2s ease;
}

.save-btn {
  background: #2563eb;
  color: white;
}

.save-btn:hover {
  background: #1d4ed8;
}

.cancel-btn {
  background: #e9ecef;
  color: #333;
}

.cancel-btn:hover {
  background: #dee2e6;
}

@keyframes fadeIn {
  from { opacity: 0; transform: scale(0.95); }
  to { opacity: 1; transform: scale(1); }
}
</style>
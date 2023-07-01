<script>
export default {
  name: 'App',
  data()
  {
    return {
      data:[],
      selected: null,
      value:""
    }
  },
  methods: {
    generateData(){
      for(let i = 1; i <= 20; i++)
      {
        this.data.push({
          name: 'foo' + i,
          value: 'bar' + i,
          id: i
        })
      }
    },
    edit(id)
    {
      this.selected = id;
    },
    save(e)
    {
      e.preventDefault();
      this.data = this.data.map(el =>{
        if(el.id === this.selected)
        {
          return {
            ...el,
            value: this.value
          }
        }
        else return el;
      })
      this.selected = null;
      this.value = "";
    }
  },
  created()
  {
    this.generateData();
  }
}
</script>

<template>
 <div class="container">
    <div class="item" v-for="item in data" :key="item.id">
      <div v-if="item.id !== selected">
        <div class="name">Name: {{ item.name }}</div>  
        <div class="value">Value: {{ item.value }}</div>
        <img src="./edit.png" @click="edit(item.id)" alt="">
      </div>
      <div v-else>
        <form>
          <label>Name: </label><input :value="item.name" type="text" disabled />
          <label>Value: </label><input v-model="value" type="text" />
          <div class="save">
            <button type="submit" @click="save">Сохранить</button>
          </div>
        </form>
      </div>
    </div>
 </div>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Rubik:wght@300;400;500&display=swap');

.container
{
  width: 400px;
  margin:0 auto;
}

.item
{
  position: relative;
  font-family: 'Rubik', sans-serif;
  font-size: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  width: 100%;
  height: 200px;
  text-align: center;
  border: 1px solid rgb(255, 255, 255);
  border-radius: 10px;
  margin-bottom: 20px;
  background-color: rgb(185, 180, 180);
  color: white;
}
img 
{
  position: absolute;
  top: 10px;
  right: 10px;
}
form input
{
  font-family: 'Rubik', sans-serif;
  display: flex;
  flex-direction: column;
  border: none;
  outline: none;
  background-color: rgb(255, 255, 255);
  border-radius: 5px;
  padding: 10px;
}
label
{
  text-align: left;
  width: 173px;
  display: inline-block;
}
button[type="submit"]
{
  outline: none;
  border: none;
  border-radius: 5px;
  padding: 10px 15px;
  text-align: left;
  margin-top: 15px;
}
.save
{
  width: 173px;
  display: flex;
  justify-content:flex-start;
}
</style>

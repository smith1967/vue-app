<template>
  <div>
    <h1 v-if="ok">ชื่อ: {{upperName}}</h1>
    <h2 v-show="ok">ชื่อ: {{newName}}</h2>
    <h3>อายุ: {{age+10}}</h3>
    <input type="text" :value="name.trim().toUpperCase()">
    <br>
    <input type="text" v-model="members.name">
    <br>
    <input type="text" v-model="members.org">
    <br>
    <button @click="doSave">Save</button>
    <br>
    <button @click="doToggle">Toggle</button>
    <br>
    <table>
      <thead>
        <tr>
          <th>ลำดับ</th>
          <th>ชื่อ</th>
          <th>หน่วยงาน</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="m in members" :key="m.id" class="text" :class="{gray: m.id % 2}">
          <td>{{m.id}}</td>
          <td>{{m.name}}</td>
          <td>{{m.org}}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<script>
export default {
  data() {
    return {
      name: "smith",
      age: 25,
      ok: true,
      members: [
        {
          id: 1,
          name: "Smith",
          org: "Tech-01"
        },
        {
          id: 2,
          name: "Oak",
          org: "Tech-02"
        },
        {
          id: 3,
          name: "Wor",
          org: "Tech-03"
        }
      ]
    };
  },
  computed: {
    upperName() {
      return this.name.toUpperCase();
    },
    newName() {
      var tmp = this.name.split(" ");
      if (tmp.length > 1) {
        return tmp[0] + " " + tmp[1].substr(0, 1);
      } else {
        return tmp[0];
      }
    }
  },
  methods: {
    doSave() {
      let id = this.members.length + 1;
      let org = this.members.org + "0" + id;
      this.members.push({
        id: id,
        name: this.members.name + id,
        org: org
      });
    },
    doSave2() {
      this.name = this.newName;
      this.doSave();
    },
    doToggle() {
      this.ok = !this.ok;
    }
  }
};
</script>
<style>
.text {
  color: blue;
}
.gray {
  background-color: #eee;
}
</style>

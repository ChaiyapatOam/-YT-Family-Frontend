<template>
  <div class="container" style="width: 400px">
    <div class="card deck">
      <div
        class="card-header d-flex justify-content-between align-items-center text-center align-center"
      >
        <h3 class="card-title">{{ user.name }}</h3>
        <span v-if="user.purchased" class="btn btn-success">จ่ายแล้ว</span>
        <span v-else class="btn btn-danger">ยังไม่จ่าย</span>
      </div>
      <div class="card-body">
        <div class="card-text">
          <!-- Some example text some example text. Jane Doe is an architect and
          engineer -->
          <ul class="list-group mb-3">
            <li
              class="list-group-item d-flex justify-content-between lh-sm"
            >
              <div>
                <h5 class="my-0">{{ user.details }}</h5>
              </div>
              <!-- <span class="text-muted">{{ user.price }}</span> -->
            </li>

            <li class="list-group-item d-flex justify-content-between">
              <h5 class="text">รวม</h5>
              <strong>{{ user.price }}</strong>
            </li>
          </ul>
        </div>
      </div>
      <!-- Form Upload image -->
      <form v-if="!user.purchased" @click="openfile">
        <input
          type="file"
          ref="file"
          @change="onFileChange"
          style="display: none"
        />
        <font-awesome-icon
          icon="fa-solid fa-cloud-upload-alt"
          style="font-size: 50px; color: #6990f2"
          class="icon"
        >
        </font-awesome-icon>
        <p>Browe File to Upload</p>
      </form>
      <!-- Preview image -->
      <div id="preview" class="card-text" style="">
        <img v-if="url" :src="url" class="card-text" style="width: 60%" />
      </div>
      <!-- Slip image -->
      <img
        v-if="user.purchased"
        class="card-img-bottom"
        src="../assets/sample.jpeg"
        alt="Card image"
        style="width: 100%; height: 80%"
      />

      <!-- Footer Upload Button -->
      <div
        v-if="showUploadButton"
        class="card-footer d-flex justify-content-between"
      >
        <button @click="closefile" class="btn btn-danger">ยกเลิก</button>
        <button class="btn btn-info">อัพโหลด</button>
      </div>
    </div>
    <br />
  </div>
</template>
<script>
import moment from "moment";
export default {
  name: "User",
  props: ["user"],
  data() {
    return {
      showImg: false,
      showUploadButton: false,
      selectedFile: null,
      url: "",
      filename: "",
      time: "",
    };
  },
  mounted() {
    setInterval(() => {
      this.time = moment(Date()).format("dddd DD/MM/YYYY hh:mm:ss a");
    }, 100);
  },
  methods: {
    toggleImg() {
      this.showimg = !this.showimg;
    },
    openfile(e) {
      this.$refs.file.click();
    },
    closefile() {
      this.url = "";
      this.showUploadButton = false;
    },
    onFileChange(e) {
      const type = e.target.files[0].type;
      console.log(type);
      if (type == "image/jpeg" || type == "image/png") {
        const file = e.target.files[0];
        this.url = URL.createObjectURL(file);
        this.showUploadButton = true;
        this.filename = e.target.files[0].name;
      } else {
        this.$swal.fire({
          type: "error",
          title: "เลือกรูปภาพสิฟะไอ่บ้านี่!!!",
          confirmButtonText: "เออๆ ก็ได้",
        });
      }
    },
    UploadFile(e) {
      this.$refs.file.click();
      this.selectedFile = e.target.files[0];
      this.filename = e.target.files[0].name;
    },
  },
};
</script>
<style scoped>
form {
  height: 160px;
  display: flex;
  cursor: pointer;
  margin: 30px 0;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  border-radius: 5px;
  border: 2px dashed #6990f2;
}
form :where(icon, p) {
  color: #6990f2;
}
form icon {
  font-size: 50px;
}
form p {
  margin-top: 15px;
  font-size: 16px;
}
</style>

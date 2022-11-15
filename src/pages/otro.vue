<template>
  <CRow :xs="{ cols: 1, gutter: 4 }" :md="{ cols: 3 }">
    <CCol xs v-for="d in data" @click="consultarUsuario(d)">
      <CCard>
        <CCardBody>
          <CCardTitle>{{ d.nombre }}</CCardTitle
          ><br />
          <CCardText
            >This is a wider card with supporting text below as a natural
            lead-in to additional content. This content is a little bit
            longer.</CCardText
          >
        </CCardBody>
        <CCardFooter
          ><small class="text-muted"
            >Last updated 3 mins ago</small
          ></CCardFooter
        >
      </CCard>
    </CCol>
  </CRow>
</template>
<script>
import { CRow, CCard, CCol } from "@coreui/bootstrap-vue";
export default {
  components: {
    CRow,
    CCard,
    CCol,
  },
  data() {
    return {
      registerActive: false,
      emptyFields: false,
      data: [],
    };
  },
  methods: {
    getClasses(index) {
      var remainder = index % 3;
      if (remainder === 0) {
        return "col-md col-md-offset-1";
      } else if (remainder === 2) {
        return "col-md";
      } else {
        return "col-md";
      }
    },
    async consultarUsuario(d) {
      let url = "https://secret-tundra-95853.herokuapp.com/usuarios/" + d._id;
      let response = await fetch(url);
      let promise = await response.json();
      let datos = promise.info;
    },
  },
  async mounted() {
    let url = "https://secret-tundra-95853.herokuapp.com/usuarios";
    let response = await fetch(url);
    let promise = await response.json();
    let datos = promise.info;
    this.data = datos;
    console.log(datos);
  },
};
</script>

<template>
  <div class="generator">
    <div id="header">
      <b-navbar type="dark" variant="dark">
        <b-navbar-nav>
          <b-nav-item href="#">CIIN adapter generator</b-nav-item>
        </b-navbar-nav>
      </b-navbar>
    </div>
    <div id="middleArea">
      <div id="toolbarLeft">
        <b-form-group
          id="fieldset-1"
          label-for="input-1"
        >
          <!--adapter name-->
          <b-form-input
            id="input-1"
            placeholder="adapter name"
            v-model="adapterName"
            trim
          ></b-form-input>
          <hr/>
          <!--adapter type-->
          <div id="adapterTypeDiv">
            <b-form-group
            >
              <b-form-radio
                v-model="adapterType"
                name="some-radios"
                value="source"
                >Source</b-form-radio
              >
              <b-form-radio
                v-model="adapterType"
                name="some-radios"
                value="sink"
                >Sink</b-form-radio
              >
            </b-form-group>
          </div>
        </b-form-group>
        <hr/>
        <!--Generate button-->
        <b-button v-on:click="generateConfig">Generate!</b-button>
      </div>
      <div id="toolbarRight">
        <b-card id="configTextCard" class="mt-3" header="YAML config:">
          <pre class="m-0" align="left">{{ configText }}</pre>
        </b-card>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Generator",
  data() {
    return {
      configText: 'YAML config will be generated here...',
      adapterName: '',
      adapterType: ''
    };
  },
  methods: {
    init() {},
    generateConfig() {
        console.log("+++ generate config:");
        console.log("adapter name: " + this.$data.adapterName);
        console.log("adapter type: " + this.$data.adapterType);
        var configText = 'adapter:\n\tname: ' + this.$data.adapterName;
        configText = configText + '\n\ttype: ' + this.$data.adapterType;
        this.$data.configText = configText;
    }
  },
  mounted() {
    this.init();
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#header {
}
#middleArea {
  display: table;
  width: 100%;
  table-layout: fixed;
  border-spacing: 10px;
  height: 500px;
  margin-top: 20px;
}
#toolbarLeft {
  display: table-cell;
  padding: 20px;
  width: 50%;
}
#toolbarRight {
  display: table-cell;
  width: 50%;
}
#configTextCard {
  position: absolute !important;
  width: 45%;
  height: 75%;
}
#configTextForm {
  text-align: left;
  width: 100%;
}
#adapterTypeDiv {
    margin-top: 20px;
    text-align: left;
}
</style>
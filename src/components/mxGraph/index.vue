<template>
  <div class="graphContainer">
    <div id="graphContainer"></div>
  </div>
</template>

<script>
  export default {
    name: "index",
    methods: {
      init() {
        const editorUiInit = EditorUi.prototype.init;

        EditorUi.prototype.init = function () {
          editorUiInit.apply(this, arguments);
          this.actions.get('export').setEnabled(true);

          // Updates action states which require a backend
          // if (!Editor.useLocalStorage) {
          //   mxUtils.post(OPEN_URL, '', mxUtils.bind(this, function (req) {
          //     const enabled = req.getStatus() !== 404;
          //     this.actions.get('open').setEnabled(enabled || Graph.fileSupport);
          //     this.actions.get('import').setEnabled(enabled || Graph.fileSupport);
          //     this.actions.get('save').setEnabled(enabled);
          //     this.actions.get('saveAs').setEnabled(enabled);
          //     this.actions.get('export').setEnabled(enabled);
          //   }));
          // }
        };

        // Adds required resources (disables loading of fallback properties, this can only
        // be used if we know that all keys are defined in the language specific file)
        mxResources.loadDefaultBundle = false;
        let bundle = mxResources.getDefaultBundle(RESOURCE_BASE, mxLanguage) ||
          mxResources.getSpecialBundle(RESOURCE_BASE, mxLanguage);

        // Fixes possible asynchronous requests
        mxUtils.getAll([bundle, STYLE_PATH + '/default.xml'], function (xhr) {
          // Adds bundle text to resources
          mxResources.parse(xhr[0].getText());

          // Configures the default graph theme
          let themes = {};
          themes[Graph.prototype.defaultThemeName] = xhr[1].getDocumentElement();

          // Main
          let graphContainer = document.getElementById('graphContainer');
          if (graphContainer) {
            new EditorUi(new Editor(urlParams['chrome'] === '0', themes), graphContainer);
          }
        }, function () {
          document.body.innerHTML = '<center style="margin-top:10%;">Error loading resource files. Please check browser console.</center>';
        });
      }
    },
    mounted() {
      this.init();
    }
  }
</script>

<style scoped>
  .graphContainer {
    width: 100%;
    height: 100%;
    box-sizing: border-box;
  }

  .graphContainer #graphContainer {
    width: 100%;
    height: 100%;
    position: relative;
    border-radius: 4px;
    overflow: hidden;
  }
</style>

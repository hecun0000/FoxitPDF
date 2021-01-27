<template>
  <div ref="viewer" class="viewer-container"></div>
</template>
<script>
import * as UIExtension from '../foxit-lib/UIExtension.full.js'
import '../foxit-lib/UIExtension.css';

// import filePropertyAddon from '../foxit-lib/uix-addons/file-property/addon.info.json';
// import multiMediaAddon from '../foxit-lib/uix-addons/multi-media/addon.info.json';
// import passwordProtectAddon from '../foxit-lib/uix-addons/password-protect/addon.info.json';
// import redactionAddon from '../foxit-lib/uix-addons/redaction/addon.info.json';
// import pathObjectsAddon from '../foxit-lib/uix-addons/path-objects/addon.info.json';
// import printAddon from '../foxit-lib/uix-addons/print/addon.info.json';
// import fullScreenAddon from '../foxit-lib/uix-addons/full-screen/addon.info.json';
// import importFormAddon from '../foxit-lib/uix-addons/import-form/addon.info.json';
// import exportFormAddon from '../foxit-lib/uix-addons/export-form/addon.info.json';
// import undoRedoAddon from '../foxit-lib/uix-addons/undo-redo/addon.info.json';
// import textObjectAddon from '../foxit-lib/uix-addons/text-object/addon.info.json';
// import thumbnailAddon from '../foxit-lib/uix-addons/thumbnail/addon.info.json';

export default {
    mounted() {
        const libPath = '/foxit-lib/';
        this.pdfui = new UIExtension.PDFUI({
            i18n: {
              lng: 'zh-CN'
            },
            viewerOptions: {
                libPath,
                jr: {
                    readyWorker: window.readyWorker
                }
            },
            renderTo: this.$refs.viewer,
            appearance: UIExtension.appearances.Appearance.extend({
              getLayoutTemplate: function() {
              return [
      '        <webpdf>
      '      <div class="fv__ui-mobile-header" name="fv--mobile-header">
      '          <div class="fv__ui-mobile-header-right" name="fv--mobile-header-right" style="margin-left: auto;">
      '              <hand-button icon-class="fv__icon-mobile-topbar-hand"></hand-button>
      '              <mobile:pageview-dropdown name="fv--mobile-pageview-dropdown">
      '                  <single-page-button></single-page-button>
      '                  <continuous-page-button></continuous-page-button>
      '              </mobile:pageview-dropdown>
      '              <dropdown class="fv__ui-mobile-topbar-tools-dropdown fv__ui-dropdown-hide-text" name="fv--mobile-topbar-tools-dropdown" @cannotBeDisabled>
      '                  <open-localfile-button @cannotBeDisabled></open-localfile-button>
      '                  <open-fromurl-button @cannotBeDisabled></open-fromurl-button>
      '                  <print:print-button></print:print-button>
      '                  <download-file-button></download-file-button>
      '                  <full-screen:toggle-full-screen-button name="fv--toggle-full-screen-button" @hide-on-device="ios"></full-screen:toggle-full-screen-button>
      '                  <fpmodule:file-property-button name="fv--file-property-button"></fpmodule:file-property-button>
      '              </dropdown>
      '          </div>
      '      </div>
      '      <div class="fv__ui-body">
      '          <viewer @zoom-on-pinch @zoom-on-doubletap @touch-to-scroll></viewer>
      '      </div>
      '      <template name="template-container">
      '          <create-stamp-dialog></create-stamp-dialog>
      '          <print:print-dialog></print:print-dialog>
      '          <loupe-tool-dialog></loupe-tool-dialog>
      '          <create-ink-sign-dialog></create-ink-sign-dialog>
      '          <distance:measurement-popup></distance:measurement-popup>
      '          <fpmodule:file-property-dialog></fpmodule:file-property-dialog>
      '          <redaction:redaction-page-dialog></redaction:redaction-page-dialog>
      '          <!-- contextmenus -->
      '          <page-contextmenu></page-contextmenu>
      '          <default-annot-contextmenu></default-annot-contextmenu>
      '          <markup-contextmenu></markup-contextmenu>
      '          <markup-contextmenu name="fv--line-contextmenu"></markup-contextmenu>
      '          <markup-contextmenu name="fv--linearrow-contextmenu"></markup-contextmenu>
      '          <markup-contextmenu name="fv--polylinedimention-contextmenu"></markup-contextmenu>
      '          <markup-contextmenu name="fv--polygondimension-contextmenu"></markup-contextmenu>
      '          <markup-contextmenu name="fv--circle-contextmenu"></markup-contextmenu>
      '          <markup-contextmenu name="fv--square-contextmenu"></markup-contextmenu>
      '          <markup-contextmenu name="fv--polyline-contextmenu"></markup-contextmenu>
      '          <markup-contextmenu name="fv--polygon-contextmenu"></markup-contextmenu>
      '          <markup-contextmenu name="fv--polygoncloud-contextmenu"></markup-contextmenu>
      '          <markup-contextmenu name="fv--ink-contextmenu"></markup-contextmenu>
      '          <markup-contextmenu name="fv--stamp-contextmenu"></markup-contextmenu>
      '          <markup-contextmenu name="fv--text-contextmenu"></markup-contextmenu>
      '          <markup-contextmenu name="fv--areahighlight-contextmenu"></markup-contextmenu>
      '          <markup-contextmenu name="fv--replace-contextmenu"></markup-contextmenu>
      '          <measurement-contextmenu></measurement-contextmenu>
      '          <default-annot-contextmenu name="fv--caret-contextmenu"></default-annot-contextmenu>
      '          <textmarkup-contextmenu name="fv--highlight-contextmenu"></textmarkup-contextmenu>
      '          <textmarkup-contextmenu name="fv--strikeout-contextmenu"></textmarkup-contextmenu>
      '          <textmarkup-contextmenu name="fv--underline-contextmenu"></textmarkup-contextmenu>
      '          <textmarkup-contextmenu name="fv--squiggly-contextmenu"></textmarkup-contextmenu>
      '          <freetext-contextmenu name="fv--typewriter-contextmenu"></freetext-contextmenu>
      '          <freetext-contextmenu name="fv--callout-contextmenu"></freetext-contextmenu>
      '          <freetext-contextmenu name="fv--textbox-contextmenu"></freetext-contextmenu>
      '          <action-annot-contextmenu name="fv--image-contextmenu"></action-annot-contextmenu>
      '          <action-annot-contextmenu name="fv--link-contextmenu"></action-annot-contextmenu>
      '          <comment-card-contextmenu></comment-card-contextmenu>
      '          <fileattachment-contextmenu></fileattachment-contextmenu>
      '          <media-contextmenu></media-contextmenu>
      '          <sound-contextmenu></sound-contextmenu>
      '          <redact-contextmenu></redact-contextmenu>
      '      </template>
      '  </webpdf>
              ].join('');
              }
            })
        });
    }
}
</script>
<style>
.viewer-container,
.viewer-container > .fv__ui-webpdf {
  height: 100%;
}
</style>

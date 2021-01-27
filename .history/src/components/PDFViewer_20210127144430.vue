<template>
  <div ref="viewer" class="viewer-container"></div>
</template>
<script>
import * as UIExtension from '../foxit-lib/UIExtension.full.js'
import '../foxit-lib/UIExtension.css';

import filePropertyAddon from '../foxit-lib/uix-addons/file-property/addon.info.json';
import multiMediaAddon from '../foxit-lib/uix-addons/multi-media/addon.info.json';
import passwordProtectAddon from '../foxit-lib/uix-addons/password-protect/addon.info.json';
import redactionAddon from '../foxit-lib/uix-addons/redaction/addon.info.json';
import pathObjectsAddon from '../foxit-lib/uix-addons/path-objects/addon.info.json';
import printAddon from '../foxit-lib/uix-addons/print/addon.info.json';
import fullScreenAddon from '../foxit-lib/uix-addons/full-screen/addon.info.json';
import importFormAddon from '../foxit-lib/uix-addons/import-form/addon.info.json';
import exportFormAddon from '../foxit-lib/uix-addons/export-form/addon.info.json';
import undoRedoAddon from '../foxit-lib/uix-addons/undo-redo/addon.info.json';
import textObjectAddon from '../foxit-lib/uix-addons/text-object/addon.info.json';
import thumbnailAddon from '../foxit-lib/uix-addons/thumbnail/addon.info.json';

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
            addons: [
                filePropertyAddon,
                multiMediaAddon,
                passwordProtectAddon,
                redactionAddon,
                pathObjectsAddon,
                printAddon,
                fullScreenAddon,
                importFormAddon,
                exportFormAddon,
                undoRedoAddon,
                thumbnailAddon
            ].concat(
                UIExtension.PDFViewCtrl.DeviceInfo.isMobile
                    ? []
                    : textObjectAddon
            )
            appearance: UIExtension.appearances.Appearance.extend({
              getLayoutTemplate: function() {
              return [
'              <webpdf>',
'    <toolbar name="toolbar" class="fv__ui-toolbar-scrollable">',
'                <group-list name="home-toolbar-group-list">',
// '                    <group name="home-tab-group-hand" retain-count="3">',
// '                        <hand-button></hand-button>',
// '                        <selection-button></selection-button>',
// '                        <snapshot-button @hide-on-sr></snapshot-button>',
// '                    </group>',
// '                    <group name="home-tab-group-change-color" @hide-on-sr>',
// '                        <change-color-dropdown></change-color-dropdown>',
// '                    </group>',
'                    <group name="home-tab-group-io" retain-count="1" shrink-title="toolbar.more.document.title">',
'                        <open-file-dropdown></open-file-dropdown>',
'                        <download-file-button></download-file-button>',
'                        <print:print-button></print:print-button>',
'                    </group>',
'                    <group name="home-tab-group-nav" retain-count="3">',
'                        <goto-prev-page-button></goto-prev-page-button>',
'                        <goto-next-page-button></goto-next-page-button>',
'                        <goto-page-input></goto-page-input>',
'                    </group>',
'                    <group name="home-tab-group-zoom">',
'                        <zoom-out-button></zoom-out-button>',
'                        <zoom-in-button></zoom-in-button>',
'                        <editable-zoom-dropdown></editable-zoom-dropdown>',
'                    </group>',
'                    <group name="comment-tab-group-drawing" retain-count="2">',
'                        <create-drawings-dropdown></create-drawings-dropdown>  ',
'                        <create-area-highlight-button></create-area-highlight-button>',
'                    </group>',
'                    <group name="comment-tab-group-pencil" retain-count="2">',
'                        <create-pencil-button></create-pencil-button>',
'                        <eraser-button></eraser-button>',
'                    </group>',
'                </group-list>',
'            </paddle>',
'    </toolbar>',
'    <div class="fv__ui-body">',
'        <sidebar name="sidebar" @controller="sidebar:SidebarController">',
'            <bookmark-sidebar-panel></bookmark-sidebar-panel>',
'            <commentlist-sidebar-panel>',
'                <slot for="header">',
'                    <comment-list:toggle-commentlist-group-button></comment-list:toggle-commentlist-group-button>',
'                    <dropdown separate="false" class="comment-list-dropdown" icon-class="fv__icon-toolbar-more">',
'                        <!-- <comment-list:expand-pages-button></comment-list:expand-pages-button>',
'                        <comment-list:collapse-pages-button></comment-list:collapse-pages-button> -->',
'                        <comment-list:show-comment-button></comment-list:show-comment-button>',
'                        <comment-list:hide-comment-button></comment-list:hide-comment-button>',
'                        <comment-list:import-comment-button></comment-list:import-comment-button>',
'                        <dropdown-item class="fv__ui-dropdown-container-item">',
'                            <comment-list:export-comment-dropdown></comment-list:export-comment-dropdown>',
'                        </dropdown-item>',
'                        <dropdown-item class="fv__ui-dropdown-container-item">',
'                            <comment-list:sort-comments-dropdown></comment-list:sort-comments-dropdown>',
'                        </dropdown-item>',
'                    </dropdown>',
'                </slot>',
'            </commentlist-sidebar-panel>',
'            <thumbnail-sidebar-panel></thumbnail-sidebar-panel>',
'            <layer-sidebar-panel @hide-on-sr></layer-sidebar-panel>',
'            <search-sidebar-panel></search-sidebar-panel>',
'            <attachment-sidebar-panel></attachment-sidebar-panel>',
'        </sidebar>',
'        <distance:ruler-container name="pdf-viewer-container-with-ruler">',
'            <slot>',
'                <viewer @zoom-on-pinch @zoom-on-doubletap @zoom-on-wheel @touch-to-scroll></viewer>',
'            </slot>',
'        </distance:ruler-container>',
'    </div>',
'    <template name="template-container">',
'        <create-stamp-dialog></create-stamp-dialog>',
'        <print:print-dialog></print:print-dialog>',
'        <loupe-tool-dialog></loupe-tool-dialog>',
'        <create-ink-sign-dialog></create-ink-sign-dialog>',
'        <distance:measurement-popup></distance:measurement-popup>',
'        <fpmodule:file-property-dialog></fpmodule:file-property-dialog>',
'        <redaction:redaction-page-dialog @hide-on-sr></redaction:redaction-page-dialog>',
'        <!-- contextmenus -->',
'        <page-contextmenu></page-contextmenu>',
'        <default-annot-contextmenu></default-annot-contextmenu>',
'        <markup-contextmenu></markup-contextmenu>',
'        <markup-contextmenu name="fv--line-contextmenu"></markup-contextmenu>',
'        <markup-contextmenu name="fv--linearrow-contextmenu"></markup-contextmenu>',
'        <markup-contextmenu name="fv--linedimension-contextmenu"></markup-contextmenu>',
'        <markup-contextmenu name="fv--polylinedimention-contextmenu"></markup-contextmenu>',
'        <markup-contextmenu name="fv--polygondimension-contextmenu"></markup-contextmenu>',
'        <markup-contextmenu name="fv--circle-contextmenu"></markup-contextmenu>',
'        <markup-contextmenu name="fv--square-contextmenu"></markup-contextmenu>',
'        <markup-contextmenu name="fv--polyline-contextmenu"></markup-contextmenu>',
'        <markup-contextmenu name="fv--polygon-contextmenu"></markup-contextmenu>',
'        <markup-contextmenu name="fv--polygoncloud-contextmenu"></markup-contextmenu>',
'        <markup-contextmenu name="fv--ink-contextmenu"></markup-contextmenu>',
'        <markup-contextmenu name="fv--stamp-contextmenu"></markup-contextmenu>',
'        <markup-contextmenu name="fv--text-contextmenu"></markup-contextmenu>',
'        <caret-contextmenu name="fv--areahighlight-contextmenu"></caret-contextmenu>',
'        <caret-contextmenu name="fv--replace-contextmenu"></caret-contextmenu>',
'        <measurement-contextmenu></measurement-contextmenu>',
'        <caret-contextmenu name="fv--caret-contextmenu"></caret-contextmenu>',
'        <textmarkup-contextmenu name="fv--highlight-contextmenu"></textmarkup-contextmenu>',
'        <textmarkup-contextmenu name="fv--strikeout-contextmenu"></textmarkup-contextmenu>',
'        <textmarkup-contextmenu name="fv--underline-contextmenu"></textmarkup-contextmenu>',
'        <textmarkup-contextmenu name="fv--squiggly-contextmenu"></textmarkup-contextmenu>',
'        <freetext-contextmenu name="fv--typewriter-contextmenu"></freetext-contextmenu>',
'        <freetext-contextmenu name="fv--callout-contextmenu"></freetext-contextmenu>',
'        <freetext-contextmenu name="fv--textbox-contextmenu"></freetext-contextmenu>',
'        <action-annot-contextmenu name="fv--image-contextmenu"></action-annot-contextmenu>',
'        <action-annot-contextmenu name="fv--link-contextmenu"></action-annot-contextmenu>',
'        <comment-card-contextmenu></comment-card-contextmenu>',
'        <fileattachment-contextmenu></fileattachment-contextmenu>',
'        <media-contextmenu></media-contextmenu>',
'        <sound-contextmenu></sound-contextmenu>',
'        <redact-contextmenu></redact-contextmenu>',
'        <edit-graphics:image-contextmenu></edit-graphics:image-contextmenu>',
'        <edit-pageobjects:path-contextmenu></edit-pageobjects:path-contextmenu>',
'        <field-signature-contextmenu name="fv--field-signature-contextmenu"></field-signature-contextmenu>',
'        <text-sel:text-selection-tooltip></text-sel:text-selection-tooltip>',
'        <freetext:freetext-tooltip></freetext:freetext-tooltip>',
'        <annottext name="fv--annottext-tooltip"></annottext>',
'    </template>',
'</webpdf>',
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

You can extend the **HtmlEditor**'s [formats](https://github.com/DevExpress/DevExtreme/tree/18_2/js/ui/html_editor/formats) and [modules](https://github.com/DevExpress/DevExtreme/tree/18_2/js/ui/html_editor/modules) and also Quill's [formats](https://github.com/quilljs/quill/tree/1.3.6/formats) and [modules](https://github.com/quilljs/quill/tree/1.3.6/modules). To get a format or module for further extension, pass *"formats/[formatName]"* or *"modules/[moduleName]"* to the [getModule(modulePath)](/api-reference/10%20UI%20Widgets/dxHtmlEditor/3%20Methods/getModule(modulePath).md '/Documentation/ApiReference/UI_Widgets/dxHtmlEditor/Methods/#getModulemodulePath') method.

In the following code, the `strike` format is extended so that the stricken out text is non-editable when the format is applied. The extended format is then [registered](/api-reference/10%20UI%20Widgets/dxHtmlEditor/3%20Methods/registerModules(modules).md '/Documentation/ApiReference/UI_Widgets/dxHtmlEditor/Methods/#registerModulesmodules').

---
#####jQuery

    <!--JavaScript-->
    $(function() {
        $("#htmlEditorContainer").dxHtmlEditor({
            // ...
            onInitialized: function(e) {
                var htmlEditor = e.component;
                var Strike = htmlEditor.getModule("formats/strike");
                class NonEditableStrike extends Strike {
                    // Overrides the method that creates a DOM node for the formatted text
                    static create(value) {
                        // Creates a DOM node using the parent's implementation
                        let node = super.create(value);
                        node.setAttribute('contenteditable', false);
                        return node;
                    }
                }
                // Replaces the built-in `strike` format
                htmlEditor.registerModules({ "formats/strike": NonEditableStrike });
            }
        });

    });

#####Angular

    <!--TypeScript-->
    import { DxHtmlEditorModule } from "devextreme-angular";
    // ...
    export class AppComponent {
        onInitialized (e) {
            let htmlEditor = e.component;
            let Strike = htmlEditor.getModule("formats/strike");
            class NonEditableStrike extends Strike {
                // Overrides the method that creates a DOM node for the formatted text
                static create(value) {
                    // Creates a DOM node using the parent's implementation
                    let node = super.create(value);
                    node.setAttribute('contenteditable', false);
                    return node;
                }
            }
            // Replaces the built-in `strike` format
            htmlEditor.registerModules({ "formats/strike": NonEditableStrike });
        }
    }
    @NgModule({
        imports: [
            // ...
            DxHtmlEditorModule
        ],
        // ...
    })

    <!--HTML-->
    <dx-html-editor
        (onInitialized)="onInitialized($event)">
    </dx-html-editor>

---
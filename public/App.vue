<template>
    <div id="app">
        <h1>Sharepic-Generator</h1>
        <div class="renderOptions">
            <label>URL zu einem Bild: <input v-model="imgurl"> </label><br>
            <label>Breite: <input v-model="width"> </label> <label>Höhe: <input v-model="height"> </label><br>
            <label>Faktor für die Bildauflösung: <input v-model="scale"> </label> (ergibt eine Auflösung von {{
            `${parseInt(width)*parseFloat(scale)} x ${parseInt(height)*parseFloat(scale)}` }})<br>
            <button v-on:click="save">Sharepic erstellen und herunterladen</button>
            <br><br>
        </div>
        <div class="wrapper">
            <div id="preview" class="preview" v-bind:style="previewStyle">
                <editor
                        v-bind:style="editorStyle"
                        api-key="no-api-key"
                        :init="{menubar: 'format view insert', inline:true, force_br_newlines : true,   force_p_newlines : false,   forced_root_block : '',
                plugins: [
           'advlist autolink lists link image charmap print preview anchor',
           'searchreplace visualblocks code fullscreen',
           'insertdatetime media table paste code help wordcount'
         ],
         toolbar:
           'undo redo | bold italic forecolor | alignleft aligncenter | outdent indent | formatselect fontsizeselect '}"
                        v-model="content"
                ></editor>
            </div>
        </div>
    </div>
</template>

<script>
    import Editor from "@tinymce/tinymce-vue";
    import html2canvas from "html2canvas";

    export default {
        name: "app",
        components: {
            "editor": Editor
        },
        data() {
            return {
                width: "500",
                height: "500",
                imgurl: "https://i.imgur.com/unDIqBB.png",
                scale: "1.6",
                content: "<p style=\"text-align: center;\">&nbsp;</p>\n<h1 style=\"text-align: center;\"><span style=\"font-size: 36pt; font-family: verdana, geneva, sans-serif; color: #ffffff;\">Veranstaltungs-Titel</span></h1>\n<p style=\"text-align: center;\"><span style=\"font-size: 24pt; font-family: verdana, geneva, sans-serif; color: #ffffff;\"><strong>Was?</strong> Veranstaltung</span></p>\n<p style=\"text-align: center;\"><span style=\"font-size: 24pt; font-family: verdana, geneva, sans-serif; color: #ffffff;\"><strong>Wann?</strong> 01.01.2020</span></p>\n<p style=\"text-align: center;\"><span style=\"font-size: 24pt;\"><span style=\"font-family: verdana, geneva, sans-serif; color: #ffffff;\"><strong>Wo?</strong> mumble<br /></span><span style=\"font-size: 18pt;\"><span style=\"font-family: verdana, geneva, sans-serif; color: #ffffff;\">auf </span><em><span style=\"font-family: verdana, geneva, sans-serif; color: #ffffff;\">fachschaften.uni-goettingen.de</span></em></span></span></p>"
            };
        },
        computed: {
            previewStyle() {
                return `width:${this.width}px; height:${this.height}px; background-size: ${this.width}px ${this.height}px; background-image: url("${this.imgurl}");`;
            },
            editorStyle() {
                return `width:${this.width}px; height:${this.height}px;`;
            }
        },
        methods: {
            save() {
                const element = document.getElementById("preview");
                html2canvas(element, {
                    useCORS: true,
                    scale: parseInt(this.scale),
                    // windowWidth: element.scrollWidth,
                    // windowHeight: element.scrollHeight
                }).then(function (canvas) {
                    var link = document.createElement("a");
                    link.download = "sharepic.png";
                    link.href = canvas.toDataURL();
                    link.click();
                    document.body.appendChild(link);
                });
            }
        }
    };
</script>

<style>
    .preview {
        /*background-image: url("./sharepic.png");*/
    }

    p {
        margin: 0;
        padding: 0;
    }
</style>
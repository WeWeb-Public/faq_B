<template>
<div>
    <!-- {{section}} -->
    <div class="faq_B section-side-padding container-fluid">
        <wwObject ww-category="background" :ww-object="section.data.background"></wwObject>

        <!--TOP WWOBJS-->
        <div class="top-ww-objs">
            <div class="top-ww-obj" v-for="topWwObj in section.data.topWwObjs" :key="topWwObj.uniqueId">
                <wwObject :ww-object="topWwObj"/>
                <!-- <div v-if="editingSection" class="remove-ww-obj" @click="removeWwObjFromArray(data.topWwObjs, topWwObj)"><i class="fa fa-times" aria-hidden="true"></i></div> -->
            </div>
            <!-- <div class="add-ww-obj-container">
                <div v-if="editingSection" class="add-ww-obj" @click="addWwObjToArray(data.topWwObjs)"><i class="fa fa-plus" aria-hidden="true"></i></div>
            </div> -->
        </div>

        <div class="accordion">
            <div v-for="(block, idx) in section.data.blocks" :key="block.uniqueId" class="accordion-item marginb10">
                <!-- <div v-if="editingSection" @click="removeWwObjFromArray(data.blocks, block)" class="remove-container">
                    <i class="fa fa-times" aria-hidden="true"></i>
                </div> -->
                <div v-on:click="addclick(idx)">
                    <wwObject :class="[`acc-title a-${idx}`, { active: idxActive === idx }]" :ww-object="block.faqTitle"/>
                </div>

                <!-- <transition name="slide" mode="out-in"> -->
                    <div :class="[`content content-${idx}`, { active: idxActive === idx }]" v-show="idxActive === idx">
                        <div class="block-ww-obj" v-for="contentWwObj in block.contentWwObjs" :key="contentWwObj.uniqueId">
                            <wwObject :ww-object="contentWwObj"/>
                            <!-- <div v-if="editingSection" class="remove-ww-obj" @click="removeWwObjFromArray(block.contentWwObjs, contentWwObj)"><i class="fa fa-times" aria-hidden="true"></i></div> -->
                        </div>
                        <div class="add-ww-obj-container">
                            <!-- <div v-if="editingSection" class="add-ww-obj" @click="addWwObjToArray(block.contentWwObjs)"><i class="fa fa-plus" aria-hidden="true"></i></div> -->
                        </div>
                    </div>
                <!-- </transition> -->

            </div>
            <!-- <div v-if="editingSection" class="feature-container text-center marginb20"> -->
                <!-- <div class="ww-add-block-container" @click="addWwObjToArray(data.blocks, 'newBlock')"> -->
                    <!-- Ajouter bloc -->
                <!-- </div> -->
            <!-- </div> -->
        </div>


        <!--BOTTOM WWOBJS-->
        <div class="bottom-ww-objs">
            <div class="top-ww-obj" v-for="bottomWwObj in section.data.bottomWwObjs" :key="bottomWwObj.uniqueId">
                <wwObject :ww-object="bottomWwObj"/>
                <!-- <div v-if="editingSection" class="remove-ww-obj" @click="removeWwObjFromArray(data.bottomWwObjs, bottomWwObj)"><i class="fa fa-times" aria-hidden="true"></i></div> -->
            </div>
            <!-- <div class="add-ww-obj-container">
                <div v-if="editingSection" class="add-ww-obj" @click="addWwObjToArray(data.bottomWwObjs)"><i class="fa fa-plus" aria-hidden="true"></i></div>
            </div> -->
        </div>

    </div>
</div>
</template>

<script>
export default {
	name: "faq_B",
	props: {
		section: Object
    },
    data() {
        return {
            idxActive: -1
        }
    },
	methods: {
		init () {
            this.section.data.topWwObjs = this.section.data.topWwObjs || []
            this.section.data.bottomWwObjs = this.section.data.bottomWwObjs || []
            this.section.data.blocks = this.section.data.blocks || [];
            if (this.section.data.blocks.length === 0) {
                this.section.data.blocks.push(this.getNewBlock());
            }
        },
        removeWwObjFromArray (wwObjArray, wwObj) {
            if (wwObjArray.length === 1) { return; }
            const index = wwObjArray.indexOf(wwObj);
            if (index !== -1) {
                wwObjArray.splice(index, 1);
            }
        },
        addWwObjToArray (wwObjArray, option) {
            console.log('tralala : ', wwObjArray, option)
            var objToPush = this.getNewWwObj()
            if (option === 'empty') { objToPush = {} }
            if (option === 'newBlock') { objToPush = this.getNewBlock() }
            wwObjArray.push(objToPush)
        },
        getNewBlock () {
        return {
            "faqTitle": {
            "data": {
                "children": {}
            },
            "link": {
                "data": {}, "type": "none"
            },
            "tags": [],
            "ratio": 66.66666,
            "hidden": false,
            "content": {
                "data": { "tag": "div", "font": "", "size": "text-small", "text": { "fr_FR": "Titre" }, "align": "center", "color": "#192234", "classes": [], "children": [] }, "type": "ww-text"
            },
            "children": {},
            "paddings": {},
            // "uniqueId": wwUtils.getUniqueId(),
            "wwVersion": 2
            },
            // "uniqueId": wwUtils.getUniqueId(),
            "contentWwObjs": [{
                "data": {}, "link": { "data": {}, "type": "none" }, "tags": [], "ratio": 66.66666, "hidden": false, "content": { "data": { "size": "big" }, "type": "ww-margin" }, "children": {}, "paddings": {}, 
                // "uniqueId": wwUtils.getUniqueId(), 
                "wwVersion": 2
            },{
                "data": { "children": {} }, "link": { "data": {}, "type": "none" }, "tags": [],
                "ratio": 66.66666, "hidden": false, "content": { "data": { "tag": "div", "font": "", "size": "", "text": { "en_GB": "New text", "fr_FR": "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat" }, "align": "left", "color": "#192234", "classes": [], "children": [] }, "type": "ww-text" }, "children": {}, "paddings": {}, 
                // "uniqueId": wwUtils.getUniqueId(), 
                "wwVersion": 2
            }
            ],
            // "uniqueId": wwUtils.getUniqueId()
        }
        },
        removeThumbnail (thumbnail) {
            const index = this.section.data.thumbnails.indexOf(thumbnail);
            if (index !== -1) {
                this.section.data.thumbnails.splice(index, 1);
            }
        },
        getNewWwObj (option) {
            return {
                "data": {},
                "link": { "data": {}, "type": "none" },
                "ratio": 66.66666,
                "hidden": false,
                "content": { "data": { "tag": "div", "font": "", "size": "", "text": { "en_GB": "New text", "fr_FR": "Nouveau texte" }, "align": "center", "color": "", "classes": [], "children": [] }, "type": "ww-text" },
                "children": {},
                // "uniqueId": wwUtils.getUniqueId(),
                "wwVersion": 2
            }
        },
        addclick (index) {
            this.idxActive = (this.idxActive === index) ? -1 : index;
            // contentElement.slideToggle(400);
        }
    },
    mounted: function () {
        this.init()
	}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.faq_B .container {
    width: 100%;
    position: relative;
}

.faq_B .section-padding {
    padding-bottom: 30px;
}

.faq_B .top-ww-obj,
.bottom-ww-obj {
    position: relative;
}

.faq_B .remove-ww-obj {
    position: absolute;
    top: 0;
    left: 0;
    transform: translate(-50%, -50%);
    height: 30px;
    width: 30px;
    background-color: white;
    color: #92979C;
    box-shadow: 0px 1px 1px 0px #656565;
    -moz-box-shadow: 0px 1px 1px 0px #656565;
    -webkit-box-shadow: 0px 1px 1px 0px #656565;
    border-radius: 100%;
    text-align: center;
    line-height: 30px;
    cursor: pointer;
    z-index: 2;
}

.faq_B .block-ww-obj {
    position: relative;
}

.faq_B .add-ww-obj-container {
    width: 100%;
    text-align: center;
    margin: 10px 0;
    position: relative;
}

.faq_B .add-ww-obj-container .add-ww-obj {
    display: inline-block;
    height: 40px;
    width: 40px;
    line-height: 40px;
    text-align: center;
    background-color: white;
    box-shadow: 0 1px 2px 0 rgba(0, 0, 0, 0.5);
    border-radius: 3px;
    cursor: pointer;
}

.faq_B .padding010 {
    padding: 0 10px;
}

.faq_B .section-title {
    margin-bottom: 20px;
}

.faq_B .section-subtitle {
    margin-top: 10px;
    margin-bottom: 0px;
}

.faq_B .accordion {
    display: flex;
    flex-direction: column;
    margin: 0 10%;
    padding: 0 15px
}

.faq_B .accordion .acc-title {
    position: relative;
    text-decoration: none;
    width: calc(100% - 0px);
    padding: 1rem 3rem 1rem 1rem;
    color: #7288a2;
    font-size: 1.15rem;
    font-weight: 400;
    border-bottom: 1px solid #e5e5e5;
    cursor: pointer;
}

.faq_B .accordion .acc-title.active {
    color: #7288a2;
    border-bottom: 1px solid #7288a2;
}

.faq_B .accordion .acc-title::after {
    font-family: 'FontAwesome', sans-serif;
    content: '\f067';
    position: absolute;
    float: right;
    right: -40px;
    font-size: 1rem;
    width: 30px;
    height: 30px;
    -webkit-border-radius: 50%;
    -moz-border-radius: 50%;
    border-radius: 50%;
    border: 1px solid #7288a2;
    text-align: center;
    padding: 7px 5px 5px 5px;
}

.faq_B .accordion .acc-title.active::after {
    font-family: 'FontAwesome', sans-serif;
    content: '\f068';
    color: #7288a2;
    border: 1px solid #7288a2;
    padding-top: 7px;
}

.faq_B .accordion .content {
    /* display: none; */
    display: block;
    padding: 1rem;
    border-bottom: 1px solid #e5e5e5;
    overflow: hidden;
}

.faq_B .accordion .content.hidden {
    /* height: 0!important; */
}

.faq_B .accordion .content p {
    font-size: 1rem;
    font-weight: 300;
    position: relative;
}

.faq_B .button-container {
    margin: 20px 0;
}

.faq_B .ww-add-block-container {
    position: relative;
    display: inline-block;
    height: 60px;
    width: 60px;
    box-shadow: 0 1px 2px rgba(0, 0, 0, 0.5);
    border-radius: 3px;
    color: #525252;
    cursor: pointer;
    background-color: white;
}

.faq_B .ww-add-block-container i {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    -moz-transform: translate(-50%, -50%);
    -webkit-transform: translate(-50%, -50%);
    font-size: 30px;
}

.faq_B .accordion-item {
    position: relative;
}

.faq_B .remove-container {
    position: absolute;
    background-color: white;
    -moz-box-shadow: 0px 1px 1px 0px #656565;
    -webkit-box-shadow: 0px 1px 1px 0px #656565;
    -o-box-shadow: 0px 1px 1px 0px #656565;
    box-shadow: 0px 1px 1px 0px #656565;
    width: 25px;
    height: 25px;
    border-radius: 100%;
    left: -30px;
    top: 5px;
    text-align: center;
    padding-top: 2px;
    color: #e73055;
    cursor: pointer;
}

@media (min-width: 768px) {
    .faq_B .accordion {
        margin: 0 10%;
        padding: 0 15px
    }
}

@media (min-width: 992px) {
    .faq_B .accordion {
        margin: 0 20%;
        padding: 0 15px
    }
}

@media (min-width: 1200px) {
    .faq_B .accordion {
        margin: 0 26%;
        padding: 0 15px
    }
}

.slide-enter-active,
.slide-leave-active {
  transition: opacity 1s;
}

.slide-enter,
.slide-leave-to {
  opacity: 0;
}
</style>

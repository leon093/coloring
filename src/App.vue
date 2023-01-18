<script setup>
import { ref, onMounted } from "vue";

const width = 641;
const height = 835;

const optionsStage = {
    width,
    height,
    pixelRatio: 1
};

const elStageParent = ref(null);
const elStage = ref(null);
const elLayer = ref(null);
const elGroupSvg = ref(null);
const elGroupControls = ref(null);

const defaultCircleOptions = ref({
    radius: 70,
    width: 50,
    height: 50,
    y: 200,
});

const controls = ref([
    {
        x: 20,
        fill: "#73cdfc",
        ...defaultCircleOptions.value,
    },
    {
        x: 80,
        fill: "#fce773",
        ...defaultCircleOptions.value,
    },
    {
        x: 140,
        fill: "#fc7388",
        ...defaultCircleOptions.value,
    },
    {
        x: 200,
        fill: "#fca373",
        ...defaultCircleOptions.value,
    },
    {
        x: 260,
        fill: "#a373fc",
        ...defaultCircleOptions.value,
    },
    {
        x: 320,
        fill: "#89fc73",
        ...defaultCircleOptions.value,
    },
]);

const currentColor = ref(null);

let groupControls = ref({
    x: 20,
    y: 600,
});

const defaultOptionsSvg = {
    fill: "#ddd",
    stroke: "black",
    strokeWidth: 2,
};

// svg изображение
let svgArr = ref([
    {
        ...defaultOptionsSvg,
        data: "M353 659c0,0 -10,36 11,48 19,12 21,24 10,43 0,0 25,-29 3,-44 -19,-13 -16,-33 -10,-42 7,-9 -14,-5 -14,-5z",
    },
    {
        ...defaultOptionsSvg,
        data: "M90 232c-11,3 -20,-3 -29,-17 0,0 11,25 28,25 0,0 1,-1 1,-1 2,-1 2,-4 0,-7z",
    },
    {
        ...defaultOptionsSvg,
        data: "M192 2c-100,-15 -183,87 -164,180 0,0 75,47 62,57 -16,12 -36,6 -22,22 12,14 43,30 82,36 41,-71 115,-120 201,-126 -7,-69 -41,-152 -159,-169zm-89 103c-8,22 -20,37 -28,34 -7,-3 -7,-24 1,-46 7,-21 20,-37 27,-34 8,4 8,24 0,46z",
    },
    {
        ...defaultOptionsSvg,
        data: "M144 309c-33,-13 -55,-12 -59,-16 -11,-10 -27,-38 -55,-43 -2,6 -3,11 -3,17 -3,-2 -6,-1 -11,-1 -2,3 -2,12 -3,16 -3,-1 -7,-1 -12,-1 -4,42 18,65 22,70 8,9 23,21 52,9 13,-2 28,10 45,26 4,-28 12,-54 24,-77z",
    },
    {
        ...defaultOptionsSvg,
        data: "M538 605c11,16 17,29 22,28 15,-2 44,-18 72,-6 -2,6 -4,11 -8,16 4,1 6,3 11,6 -1,4 -5,12 -7,16 3,1 7,3 11,6 -18,47 -79,69 -85,72 -19,8 -65,23 -73,-25 -3,-30 -13,-48 -28,-61 32,-11 61,-29 85,-52z",
    },
    {
        ...defaultOptionsSvg,
        data: "M136 517c-23,6 -40,16 -44,12 -10,-11 -24,-41 -53,-48 -3,5 -4,10 -4,17 -4,-2 -7,-2 -12,-2 -2,3 -3,12 -4,17 -3,-1 -8,-2 -13,-2 -14,48 21,103 24,108 11,19 38,58 73,25 44,-47 84,-33 127,-11 3,1 5,2 7,2 -45,-27 -81,-69 -101,-118z",
    },
    {
        ...defaultOptionsSvg,
        data: "M619 421c0,139 -113,251 -251,251 -2,0 -3,0 -5,0 1,-3 3,-6 4,-8 7,-9 -14,-5 -14,-5 0,0 -1,6 -2,13 -131,-9 -234,-118 -234,-251 0,-138 112,-250 251,-250 138,0 251,112 251,250zm-24 23c0,79 24,-22 0,0zm-6 1l-68 -40 -67 39 0 79 67 39c17,-10 33,-19 49,-28 6,-8 26,-50 19,-89zm-65 122l0 20c-4,0 90,-83 0,-20zm-141 73c-3,11 133,-37 135,-48l0 -25 -67 -39 -68 39 0 73zm184 -349c-27,-41 -114,-90 -114,-90l0 77 68 39 46 -26zm-189 -102c-15,0 -62,9 -66,11l0 78 68 39 67 -39 0 -78c-1,-1 -62,-11 -69,-11zm-188 100l49 28 67 -39 0 -78c-14,-7 -130,82 -116,89zm46 33c-5,-2 -49,-28 -49,-28 -22,35 -34,76 -34,120 0,23 -2,16 15,26l68 -39 0 -79zm-82 116c0,0 12,53 12,52l0 -45 -12 -7zm17 6c0,91 4,81 68,118l68 -39 0 -78 -68 -40 -68 39zm19 94l0 0c11,18 46,52 46,52l0 -23 -44 -26c-1,-1 -2,-1 -2,-3zm52 56c-10,8 124,55 135,46l0 -73 -67 -39 -68 39 0 27zm0 -193l68 39 67 -39 0 -79 -68 -39 -67 39 0 79zm206 122l0 -78 -68 -40 -68 39 0 79 68 39 68 -39 0 0zm-65 -122l68 39 67 -39 0 -79 -68 -39 -67 39 0 79 0 0zm221 13c0,-41 -34,-119 -34,-118l-46 26 0 79 68 39c15,-9 12,-3 12,-26z",
    },
    {
        ...defaultOptionsSvg,
        data: "M595 444c0,79 24,-22 0,0z",
    },
    {
        ...defaultOptionsSvg,
        data: "M589 445l-68 -40 -67 39 0 79 67 39c17,-10 33,-19 49,-28 6,-8 26,-50 19,-89z",
    },
    {
        ...defaultOptionsSvg,
        data: "M524 567l0 20c-4,0 90,-83 0,-20z",
    },
    {
        ...defaultOptionsSvg,
        data: "M383 640c-3,11 133,-37 135,-48l0 -25 -67 -39 -68 39 0 73z",
    },
    {
        ...defaultOptionsSvg,
        data: "M567 291c-27,-41 -114,-90 -114,-90l0 77 68 39 46 -26z",
    },
    {
        ...defaultOptionsSvg,
        data: "M378 189c-15,0 -62,9 -66,11l0 78 68 39 67 -39 0 -78c-1,-1 -62,-11 -69,-11z",
    },
    {
        ...defaultOptionsSvg,
        data: "M190 289l49 28 67 -39 0 -78c-14,-7 -130,82 -116,89z",
    },
    {
        ...defaultOptionsSvg,
        data: "M236 322c-5,-2 -49,-28 -49,-28 -22,35 -34,76 -34,120 0,23 -2,16 15,26l68 -39 0 -79z",
    },
    {
        ...defaultOptionsSvg,
        data: "M154 438c0,0 12,53 12,52l0 -45 -12 -7z",
    },
    {
        ...defaultOptionsSvg,
        data: "M171 444c0,91 4,81 68,118l68 -39 0 -78 -68 -40 -68 39z",
    },
    {
        ...defaultOptionsSvg,
        data: "M190 538l0 0c11,18 46,52 46,52l0 -23 -44 -26c-1,-1 -2,-1 -2,-3z",
    },
    {
        ...defaultOptionsSvg,
        data: "M242 594c-10,8 124,55 135,46l0 -73 -67 -39 -68 39 0 27z",
    },
    {
        ...defaultOptionsSvg,
        data: "M242 594c-10,8 124,55 135,46l0 -73 -67 -39 -68 39 0 27z",
    },
    {
        ...defaultOptionsSvg,
        data: "M242,401 310,440 377,401 377,322 309,283 242,322z",
    },
    {
        ...defaultOptionsSvg,
        data: "M448,523 448,445 380,405 312,444 312,523 380,562 448,523z",
    },

    {
        ...defaultOptionsSvg,
        data: "M383,401 451,440 518,401 518,322 450,283 383,322 383,401z",
    },
    {
        ...defaultOptionsSvg,
        data: "M604 414c0,-41 -34,-119 -34,-118l-46 26 0 79 68 39c15,-9 12,-3 12,-26z",
    },
    {
        ...defaultOptionsSvg,
        data: "M103 108c-7,22 -20,37 -28,34 -8,-4 -9,-24 -1,-47 0,-1 0,-1 1,-2 -7,21 -6,40 2,43 7,3 19,-9 26,-28z",
    },
    {
        ...defaultOptionsSvg,
        data: "M96 102c-4,10 -10,17 -13,16 -4,-2 -4,-11 0,-22 4,-10 9,-17 13,-16 4,2 4,11 0,22z",
    },
    {
        ...defaultOptionsSvg,
        data: "M96 102c-4,10 -10,17 -13,16 -4,-2 -4,-11 0,-22 4,-10 9,-17 13,-16 4,2 4,11 0,22z",
    },
]);

const selectedColor = (color) => (currentColor.value = color);
const repaintPath = (i) => svgArr.value[i].fill = currentColor.value;
const mouseEnter = () => (elStage.value.getNode().container().style.cursor = "pointer");
const mouseCircle = () => (elStage.value.getNode().container().style.cursor = "default");


let scaleBy = 1.01;
const zoomWheel = (e) => {
    const stage = elStage.value.getNode();
    let oldScale = stage.scaleX();
    let pointer = stage.getPointerPosition();

    let mousePointTo = {
        x: (pointer.x - stage.x()) / oldScale,
        y: (pointer.y - stage.y()) / oldScale,
    };

    let direction = e.evt.deltaY > 0 ? 1 : -1;

    if (e.evt.ctrlKey) {
        direction = -direction;
    }

    let newScale = direction > 0 ? oldScale * scaleBy : oldScale / scaleBy;

    stage.scale({ x: newScale, y: newScale });

    let newPos = {
        x: pointer.x - mousePointTo.x * newScale,
        y: pointer.y - mousePointTo.y * newScale,
    };
    stage.position(newPos);
}


// touch move
function getDistance(p1, p2) {
    return Math.sqrt(Math.pow(p2.x - p1.x, 2) + Math.pow(p2.y - p1.y, 2));
}

function getCenter(p1, p2) {
    return {
        x: (p1.x + p2.x) / 2,
        y: (p1.y + p2.y) / 2,
    };
}
let lastCenter = null;
let lastDist = 0;

const zoomMove = (e) => {
    e.evt.preventDefault();
    const stage = elGroupSvg.value.getNode();

    var touch1 = e.evt.touches[0];
    var touch2 = e.evt.touches[1];

    if (touch1 && touch2) {
        // if the stage was under Konva's drag&drop
        // we need to stop it, and implement our own pan logic with two pointers
        if (stage.isDragging()) {
            stage.stopDrag();
        }

        var p1 = {
            x: touch1.clientX,
            y: touch1.clientY,
        };
        var p2 = {
            x: touch2.clientX,
            y: touch2.clientY,
        };

        if (!lastCenter) {
            lastCenter = getCenter(p1, p2);
            return;
        }
        var newCenter = getCenter(p1, p2);

        var dist = getDistance(p1, p2);

        if (!lastDist) {
            lastDist = dist;
        }

        // local coordinates of center point
        var pointTo = {
            x: (newCenter.x - stage.x()) / stage.scaleX(),
            y: (newCenter.y - stage.y()) / stage.scaleX(),
        };

        var scale = stage.scaleX() * (dist / lastDist);

        stage.scaleX(scale);
        stage.scaleY(scale);

        // calculate new position of the stage
        var dx = newCenter.x - lastCenter.x;
        var dy = newCenter.y - lastCenter.y;

        var newPos = {
            x: newCenter.x - pointTo.x * scale + dx,
            y: newCenter.y - pointTo.y * scale + dy,
        };

        stage.position(newPos);

        lastDist = dist;
        lastCenter = newCenter;
    }
}

const zoomEnd = () => {
    lastDist = 0;
    lastCenter = null;
}

// ресайз
const resizeStage = () => {
    if (!elStage.value) return

    const stage = elStage.value.getNode();


    let containerWidth = elStageParent.value.offsetWidth; // ширина окна
    let scaleX = containerWidth / width;
    let containerHeight = window.innerHeight;
    var scaleY = containerHeight / height;


    stage.width(width * scaleX);
    stage.height(height * scaleX);
    // stage.scale({ x: scaleX, y: scaleX }); // меняем масштаб канваса

    stage.draw(); // перерисовываем канвас

    if (stage.attrs.height < window.innerHeight) {
        stage.scale({ x: scaleX, y: scaleX });
        stage.draw();
    }
};

// ориентация на мобильных устройствах
const mobileOrientation = () => {
    if (!elStage.value) return

    const stage = elStage.value.getNode();
    // const stageSize = elStage.value.getNode();
    const containerWidth = screen.width;

    const scale = containerWidth / width;
    // stage.clear();
    // stage.clearCache();

    stage.width(width * scale);
    stage.height(height * scale);
    stage.scale({ x: scale, y: scale });
    stage.draw(); // перерисовываем канвас

    if (window.orientation === 90) {
        // stage.width(width * scale);
        // stage.height(height * scale);

        const screeHeight = screen.height;
        // const scale = screeHeight / height
        const scale = screeHeight / height * 1.11

        stage.height(screeHeight);
        stage.scale({ x: scale, y: scale }); // меняем масштаб канваса

        const svgWidth = stage.attrs.width;
        elGroupControls.value.getNode().rotation(90) // переворачиваем вертикально контролы
        groupControls.value = { x: svgWidth + 100, y: 10, }; // задаем координаты где они должны стоять

        stage.draw();
        console.log('landscape')
    }
    else {

        // console.log('portrait')
        // stage.clear();
        // stage.clearCache();

        // stage.width(width * scale);
        // stage.height(height * scale);


        // stage.scale({ x: scale, y: scale }); // меняем масштаб канваса
        elGroupControls.value.getNode().rotation(0)
        groupControls.value = { x: 20, y: 600 };

    }
    stage.draw(); // перерисовываем канвас

}


window.addEventListener("resize", () => resizeStage());

// отключаем масштабирование в ios
document.addEventListener(
    "touchmove",
    (e) => {
        if (e.scale !== 1) {
            e.preventDefault();
        }
    },
    { passive: false }
);

// Прослушка события смены ориентации
window.addEventListener("orientationchange", () => mobileOrientation());

onMounted(() => {
    resizeStage()
    if (/Android|webOS|iPhone|iPad|iPod|BlackBerry|BB|PlayBook|IEMobile|Windows Phone|Kindle|Silk|Opera Mini/i
        .test(navigator.userAgent)) {

        mobileOrientation()

    }

});
</script>

<template>
    <div class="stage-parent" ref="elStageParent">
        <v-stage class="stage" :config="optionsStage" ref="elStage">
            <v-layer ref="elLayer">

                <!-- svg изображение -->
                <v-group ref="elGroupSvg" @wheel="zoomWheel" @touchmove="zoomMove" @touchend="zoomEnd">
                    <v-path :config="path" v-for="(path, i) in svgArr" :key="i" @click="repaintPath(i)" @touchstart.prevent="repaintPath(i)" />
                </v-group>

                <!-- контроллы -->
                <v-group ref="elGroupControls" :config="groupControls">
                    <v-circle v-for="(control, i) in controls" :key="i" :config="control" :stroke="
                        control.fill == currentColor
                            ? 'black'
                            : 'transparent'
                    " @touchend="selectedColor(control.fill)" @click="selectedColor(control.fill)"
                        @mouseenter="mouseEnter" @mouseleave="mouseCircle">
                    </v-circle>
                </v-group>
            </v-layer>
        </v-stage>
    </div>
</template>

<style>
.wrapper {
    position: relative;
}

.stage-parent {
    width: 100vw;
    height: 100vh;
}

.controls {
    height: 20%;
    display: flex;
    gap: 5px;
}

.controls__color {
    width: 30px;
    height: 30px;
    border-radius: 50%;
    border: 2px solid transparent;
    cursor: pointer;
}
</style>

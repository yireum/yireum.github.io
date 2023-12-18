---
layout: single
title: "VUE3에서 Drag&Drop 사용하기"
categories: vue
tags: [plugin, vuedraggable, drag&drop]
---

드래그앤드롭 기능을 사용하기 위해 플러그인을 찾아봤습니다.

이전 프로젝트에서 퍼블리싱 작업 중 드래그앤드롭이 필요한 UI가 있어 제이쿼리의 sortable 기능을 사용해봤는데,

vue3에 적용하려고 서치해보니 vuedraggable이 sortable.js에서 vue에서 사용 시 충돌을 줄이고 최적화를 위해 만든 래핑 라이브러리라고 하여 vuedraggable을 사용하기로 했습니다!

깃허브에 자세한 가이드와 사용 예제가 있어 참고하였습니다.

https://github.com/SortableJS/Vue.Draggable

- VUE draggable 설치하기
    
    ```bash
    npm i -S vuedraggable@next
    ```
    

- 코드에 적용하기
    
    ```jsx
    <template lang="">
      <section class="main_content d-flex main_view">
        <div class="layout_wrap d-flex">
          <div class="layout_box">
            <span class="store_title">상호명</span>
            <span class="category">추천메뉴</span>
            <div class="layout">
              <draggable
                v-model="layoutList"
                group="people"
                @end="onDragEnd('layoutList')"
                :animation="100"
                item-key="id"
                class="layout_menu_wrap"
              >
                <template #item="{ element }">
                  <div class="box" :class="element.type === 'B' ? 'big' : false">
                    {{ element.title }}
                  </div>
                </template>
              </draggable>
            </div>
            <!-- <div class="payment_bar"></div> -->
          </div>
          <button type="button" class="btn btn-light" data-mdb-ripple-color="dark">
            메뉴 스타일 변경
          </button>
        </div>
        <div class="menu_wrap">
          <p>등록된 상품 목록</p>
          <div class="list_wrap">
            <draggable
              v-model="menuList"
              :group="{ name: 'people', pull: 'clone', put: false }"
              :animation="100"
              item-key="id"
              class="list_box"
              :sort="false"
            >
              <template #item="{ element }">
                <div class="box" :class="element.type === 'B' ? 'big' : false">
                  {{ element.title }}
                </div>
              </template>
            </draggable>
          </div>
        </div>
      </section>
    </template>
    
    <script setup>
    import draggable from 'vuedraggable'
    
    const layoutList = ref([])
    
    const menuList = ref([
      { title: 1, type: 'S' },
      { title: 2, type: 'B' },
      { title: 3, type: 'S' },
      { title: 4, type: 'S' },
      { title: 5, type: 'S' },
      { title: 6, type: 'B' },
      { title: 7, type: 'S' },
      { title: 8, type: 'B' }
    ])
    
    const onDragEnd = (listKey) => {
      if (listKey === 'layoutList') {
        layoutList.value = [...layoutList.value]
      }
    }
    </script>
    ```
    
    - script 안에 draggable을 import하고 template 안에서 사용하면 되는데요,
    - 위의 코드는 두 개의 리스트 안에서 특정 규칙을 두고 단방향 드래그앤드롭을 위해 group 옵션을 사용하였습니다. (같은 그룹으로 묶으면 양방향 드래그앤드롭이 가능합니다!)
    - 그 외에도 sort나 animation 같은 옵션이 많은데 공유문서에 예제가 잘 나와 있어 참고하여 사용하시면 됩니다.
    - `@end="onDragEnd('layoutList')"`와 같이 내장함수도 사용할 수 있어 저는 그룹 안에서 object를 clone하여 새로운 배열에 담고 그 리스트를 저장하는 함수를 추가하였습니다.
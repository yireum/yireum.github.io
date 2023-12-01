---
layout: single
title: "Strapi Custom api 스트라피 커스텀 api"
categories: strapi
tags: [backend, strapi, server]
---

### Strapi Custom api 스트라피 커스텀 api

1. 기존 api의 controllers, services, routes에 엔드포인트 추가
    
    src/api/{model}/controllers/{model}.js
    
    ```jsx
    "use strict";
    
    const { createCoreController } = require("@strapi/strapi").factories;
    const MODEL = "api::bbs-list.bbs-list";
    
    module.exports = createCoreController(MODEL, ({ strapi }) => ({
      
      // bbs 테이블의 여러 글 수정
      async multipleUpdate(ctx) {
        const { data } = ctx.request.body;
    
        try {
          await strapi.service(MODEL).multipleUpdate(data);
          return "good";
        } catch (error) {
          console.error(error);
          return "An error occurred";
        }
      },
    
    // bbs 테이블의 여러 글 생성
      async multipleCreate(ctx) {
        const { data } = ctx.request.body;
    
        try {
          await strapi.service(MODEL).multipleCreate(data);
          return "good";
        } catch (error) {
          console.error(error);
          return "An error occurred";
        }
      },
    
      // bbs 테이블의 여러 글 삭제
      async multipleDelete(ctx) {
        const { data } = ctx.request.body;
    
        try {
          await strapi.service(MODEL).multipleDelete(data);
          return "good";
        } catch (error) {
          console.error(error);
          return "An error occurred";
        }
      },
    
      // bbs 테이블의 글 하나 생성 시 다른 배열로 받은 데이터들을 릴레이션 된 testBoard 테이블에 생성
      async multipleTableCreate(ctx) {
        const { data } = ctx.request.body;
    
        try {
          await strapi.service(MODEL).multipleTableCreate(data);
          return "good";
        } catch (error) {
          console.error(error);
          return "An error occurred";
        }
      },
    
      // bbs 테이블의 글 하나 삭제 시 릴레이션 테이블 중 testBoard 테이블들의 연관 된 글 함께 삭제
      async multipleTableDelete(ctx) {
        const { data } = ctx.request.body;
    
        try {
          await strapi.service(MODEL).multipleTableDelete(data);
          return "good";
        } catch (error) {
          console.error(error);
          return "An error occurred";
        }
      },
    }));
    ```
    

src/api/{model}/services/{model}.js

```jsx
"use strict";

/**
 * restaurant service
 */

const { createCoreService } = require("@strapi/strapi").factories;
const MODEL = "api::bbs-list.bbs-list";

module.exports = createCoreService(MODEL, ({ strapi }) => ({
  async multipleUpdate(data) {
    for (let x of data) {
      await strapi.entityService.update(MODEL, x.id, {
        data: x,
      });
    }
  },

  async multipleCreate(data) {
    for (let x of data) {
      await strapi.entityService.create(MODEL, {
        data: x,
      });
    }
  },

  async multipleDelete(ids) {
    for (let x of ids) {
      await strapi.entityService.delete(MODEL, x);
    }
  },

  async multipleTableCreate(data) {
    const result = await strapi.entityService.create(MODEL, {
      data: data.bbsData,
    });
    for (let x of data.boardData) {
      x.bbs_list = result.id;
      await strapi.api["test-board"].services["test-board"].create({ data: x });
    }
  },

  async multipleTableDelete(data) {
    const result = await strapi.entityService.findOne(MODEL, data, {
      populate: "*",
    });
    await strapi.entityService.delete(MODEL, data);
    for (let x of result.test_boards) {
      await strapi.api["test-board"].services["test-board"].delete(x.id);
    }
  },
}));
```

src/api/{model}/routes/{custom_name}.js

```jsx
module.exports = {
  routes: [
    {
      method: "PUT",
      path: "/bbs-lists/multi-update",
      handler: "bbs-list.multipleUpdate",
      config: {
        policies: [],
      },
    },
    {
      method: "POST",
      path: "/bbs-lists/multi-create",
      handler: "bbs-list.multipleCreate",
      config: {
        policies: [],
      },
    },
    {
      method: "POST",
      path: "/bbs-lists/multi-delete",
      handler: "bbs-list.multipleDelete",
      config: {
        policies: [],
      },
    },
    {
      method: "POST",
      path: "/bbs-lists/multi-table-create",
      handler: "bbs-list.multipleTableCreate",
      config: {
        policies: [],
      },
    },
    {
      method: "POST",
      path: "/bbs-lists/multi-table-delete",
      handler: "bbs-list.multipleTableDelete",
      config: {
        policies: [],
      },
    },
  ],
};
```

1. 새로운 api 생성
    1. 프로젝트 루트에서 새로운 api 생성
        
        ```bash
        yarn strapi generate
        ```
        
        api 선택 후 plugin으로 사용은 n 설정
        
    2. 새로 생긴 파일들에 코드 추가
        
        src/api/{model}/controllers/{model}.js
        
        ```jsx
        "use strict";
        
        /**
         * A set of functions called "actions" for `multi-delete`
         */
        
        module.exports = {
          async deleteMultiple(ctx) {
            const { ids } = ctx.request.body; // id 배열을 받습니다.
            for (const id of ids) {
              await strapi.api["bbs-list"].services["bbs-list"].delete(id);
            }
        
            return { message: "Posts deleted successfully" }; // 성공 메시지를 반환합니다.
          },
        };
        ```
        
        src/api/{model}/routes/{model}.js
        
        ```jsx
        module.exports = {
          routes: [
            {
              method: "POST",
              path: "/bbs-lists/delete-multiple",
              handler: "multi-delete.deleteMultiple",
              config: {
                policies: [],
              },
            },
            // 기존의 라우트 설정들은 그대로 유지하세요
          ],
        };
        ```
        

*api를 커스텀하게 만들게 되면 로우 생성 시 state가 draft로 생성이 되어 api호출 시 데이터가 안보내지는데 그럴 경우 schema.json 에서 option 설정을 수정하면 됨.

```bash
"options": {
    "draftAndPublish": false
  },
```
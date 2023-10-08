---
title: "AdvanceDialog"
date: 2021-01-20T19:00:09+08:00
author: 王书硕
---

{{< highlight tsx "linenos=table,hl_lines=5 7 13 17,linenostart=1" >}}
import { showDialog, requestDialogId, closeDialog } from '@root/common/dialog';
import { AdvanceDialog } from '@q7/micro-core-web-app/advance-dialog/index';

function renderDialog() {
  const dialogId = requestDialogId();

  showDialog(dialogId, (
    <AdvanceDialog 
      isOpen
      title="催办" 
      buttons={[{
        text: '确定',
        onClick: () => {
          closeDialog(dialogId)
        }
      }]}
      onClose={() => {
        closeDialog(dialogId)
      }} 
    >
      
    </AdvanceDialog>
  ))
}
{{< / highlight >}}

列宽可以通过鼠标拖动
```
enableColResize={true}
autoContainerWidth={false}
```


```ts
import {
  closeDialog,
  requestDialogId,
  showDialogInTab,
  showDialog,
} from "@q7/micro-core-web-app/common/dialog";
import { AdvanceDialog } from '@q7/micro-core-web-app/advance-dialog/index';
```
在tab页签内部打开dialog ———— showDialogInTab
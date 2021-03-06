# 简介
这道题有两个小问题:
1. 在 O(1) 时间内删除链表某个节点。
给定单向链表的头结点和一个节点指针, 定义一个函数在 O(1) 时间内删除该节点。
2. 删除排序链表中的重复节点。

# 实现
## 删除节点
删除链表中的节点有两种方法, 一种是使用两个指针, 分别指向要删除的节点以及被删除节点的父节点, 改变父节点 next 的指向; 第二种方法是将被删除节点的下一个节点的内容复制到当前节点, 再删除下一个节点。
对于第一种方法, 需要考虑的情况有: 头结点为空、要删除的节点为空、被删除的节点是头节点以及一般情况。
对于第二种方法, 需要考虑的情况有: 头结点为空、要删除的节点为空、要删除的节点是头结点、要删除的节点是尾结点以及一般情况。
方法一:
```js
function deleteNode(head, pToBeDeleted) {
    // 头结点为空节点或要删除的节点为空节点
    if(!head || !pToBeDeleted) {
        return head;
    }

    // 要删除的节点是头结点
    if(pToBeDeleted === head) {
        return head.next;
    }

    // 一般情况
    let pParent = head;
    let p = head.next;

    while(p) {
        if(p === pToBeDeleted) {
            pParent.next = p.next;
            break;
        }
        pParent = p;
        p = p.next;
    }

    return head;
}
```
方法二:
```js
function deleteNode(head, pToBeDeleted) {
    // 头结点为空或要删除的节点为空
    if (!head || !pToBeDeleted) {
        return head;
    }

    // 要删除的节点是头结点
    if (head === pToBeDeleted) {
        return head.next;
    }


    let p = head;

    while (p) {
        if (p === pToBeDeleted) {
            // 要删除的节点是尾结点
            if (p.next === null) {
                let pParent = head;

                // 找出被删除节点的父节点
                while (pParent.next !== p) {
                    pParent = pParent.next;
                }

                pParent.next = null;
            } else {
                p.val = p.next.val;
                p.next = p.next.next;
            }

            break;
        }

        p = p.next;
    }

    return head;
}
```

## 删除重复节点
将当前节点的值与下一个节点的值进行比较, 如果相同的话, 就改变当前节点 next 的指向。
```js
// 删除重复节点
function deleteRepeatNode(head) {
    // 链表为空或只有一个节点
    if (!head || !head.next) {
        return head;
    }

    let p = head;

    // 一般情况
    while (p && p.next) {
        if (p.val === p.next.val) {
            p.next = p.next.next;
            continue;
        }

        p = p.next;
    }

    return head;
}
```
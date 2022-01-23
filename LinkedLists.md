# Linked Lists

```
const createNode = (value) => {
  return { value: value, prev: null, next: null };
};

class LinkedList {
  constructor(head = null) {
    this.head = head;
  }

  add(newNodeValue) {
    let node = this.head;
    const newNode = createNode(newNodeValue);
    /* while loop below sets node as current tail node */
    while (node) {
      if (node.next === null) {
        break;
      }
      node = node.next;
    }
    /* newNode is now the tail node. so it's prev key shld point to node. and since node is the 2nd last node now, it's next shld point to newNode which is now the last node */
    newNode.prev = node;
    node.next = newNode;
  }

  forward() {
    let node = this.head;
    while (node) {
      console.log(node.value);
      node = node.next;
    }
  }

  bckward() {
    let node = this.head;
    /* while loop below sets node as current tail node */
    while (node) {
      if (node.next === null) {
        break;
      }
      node = node.next;
    }
    /* now tt node is the last node, loop backwards using node.prev and print node.value */
    while (node) {
      console.log(node.value);
      node = node.prev;
    }
  }
}

const node1 = createNode("turn off alarm");

const goodMornTristan = new LinkedList(node1);

goodMornTristan.add("what year is it");
goodMornTristan.add("f**k it's 11 o'clock");
goodMornTristan.add("turn on zoom on phone");
goodMornTristan.add("run into shower");
goodMornTristan.add("stream onlyFans");

console.log("Morning routine");
goodMornTristan.forward();

console.log("##########################");

console.log("Night routine");
goodMornTristan.bckward();

```

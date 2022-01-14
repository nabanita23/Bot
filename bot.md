```JS
const DirMapping = {
  west: {
    left: "south",
    right: "north",
  },
  north: {
    left: "west",
    right: "east",
  },
  south: {
    left: "east",
    right: "west",
  },
  east: {
    left: "north",
    right: "south",
  },
};

function GenGrid(size) {
  const tmp = [];
  for (let i = 0; i < size; i++) {
    for (let j = 0; j < size; j++) {
      tmp.push(`c${i},r${j}`);
    }
  }
  return tmp;
}

function GenNode() {
  return {
    direction: "",
  };
}

function GenMap(arr) {
  const tmpObj = {};
  arr.map((item) => (tmpObj[item] = new GenNode()));
  return tmpObj;
}

function getCellKey(c, r) {
  return `c${c},r${r}`;
}

function getMoveValue(cellKey) {
  // "c0,r0"
  const move = {
    c: 0,
    // n
    r: 0,
    // e
  };

  const tmp = cellKey.split(",");
  move.c = parseInt(tmp[0].substring(1));
  move.r = parseInt(tmp[1].substring(1));
  return move;
}

// Main Class start here
var Game = (function () {
  const errMsg = "Move is out of stage";
  let gridMap = null;
  let oldCell = "";
  let newCell = "";
  let stageSize = 0;
  return function () {
    const init = function (size) {
      stageSize = size;
      gridMap = new GenMap(new GenGrid(size));
      return this;
    };
    const place = function (c, r, d) {
      if (c < 0 || c > stageSize - 1 || r < 0 || r > stageSize - 1)
        throw errMsg;
      newCell = getCellKey(c, r);
      gridMap[newCell].direction = d;
      gridMap[oldCell] = new GenNode();

      oldCell = newCell;

      return this;
    };
    const left = function () {
      const oldCellDir = gridMap[oldCell].direction;
      gridMap[oldCell].direction = DirMapping[oldCellDir].left;
      return this;
    };
    const right = function () {
      gridMap[oldCell].direction = DirMapping[gridMap[oldCell].direction].right;
      return this;
    };
    const move = function () {
      const tmp = getMoveValue(oldCell);

      const oldCellDir = gridMap[oldCell].direction;
      switch (gridMap[oldCell].direction) {
        case "west":
          if (tmp.r > 0) {
            tmp.r = tmp.r - 1;
          } else {
            throw errMsg;
          }
          break;
        case "east":
          if (tmp.r < stageSize) {
            tmp.r = tmp.r + 1;
          } else {
            throw errMsg;
          }
          break;
        case "south":
          if (tmp.c > 0) {
            tmp.c = tmp.c - 1;
          } else {
            throw errMsg;
          }
          break;
        case "north":
          if (tmp.c < stageSize) {
            tmp.c = tmp.c + 1;
          } else {
            throw errMsg;
          }
          break;
      }
      place(tmp.c, tmp.r, oldCellDir);

      return this;
    };
    const report = function () {
      console.log(getMoveValue(oldCell), gridMap[oldCell].direction);
      return this;
    };
    return {
      init,
      place,
      left,
      right,
      move,
      report,
    };
  };
})();

const game = new Game();
game
  .init(5)
  .place(4, 4, "west")
  .move()
  .left()
  .move()
  .move()
  .move()
  .right()
  .right()
  .move()
  .left()
  .move()
  .move()
  .right()
  .move()
  .move()
  .report();
```

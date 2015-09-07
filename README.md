# tdd-js
The Game of life TDD JS EMAC6 





class Cell {
    constructor(isAlive = false) {
        this.neighbours = [];
        this.willLive = null;
        this.isAlive = isAlive;
    }

    setDead() {
        this.isAlive = false;
    }
    setAlive() {
        this.isAlive = true;
    }
    setSurvival() {
        const livingNeighbours = this.neighbours.reduce((living, currentCell) => {
            return living + currentCell.isAlive;
        }, 0);

        this.willLive = false;

        if ((this.isAlive && livingNeighbours === 2) || livingNeighbours === 3) {
            this.willLive = true;
        }
    }
    addNeighbour(Cell) {
        this.neighbours.push(Cell);
        Cell.neighbours.push(this);
    }
}


class World {}




describe('Cell', function() {
    // describe is a container for test cases 
    it('shoudl exist', function() {
        //it is for test cases
        assert(Cell);
    });

    it('can be instanciated', function() {
        var cell = new Cell();
        assert(cell instanceof Cell);
    });


    it('the cell can be set to DEAD', function() {
        var mycell = new Cell();
        assert.equal(mycell.isAlive, false);
    });


    it('the cell can be set to ALIVE', function() {
        var mycell = new Cell();
        mycell.setAlive();
        assert.equal(mycell.isAlive, true);
    });
    it('can have neigbour', function() {
        var mycell = new Cell();
        var neighbour = new Cell();
        mycell.addNeighbour(neighbour);
        assert.equal(mycell.neighbours[0], neighbour);
    });

    it('a living cell with less than two live neighbours dies', function() {
        var myCell = new Cell();
        myCell.setAlive();
        myCell.setSurvival();
        assert.equal(myCell.willLive, false);
    });

    it('a living cell with two or three live neighbors lives', function() {
        var myCell = new Cell();
        myCell.setAlive();
        var liveCell = new Cell();
        liveCell.setAlive();
        myCell.addNeighbour(liveCell);
        myCell.addNeighbour(liveCell);
        myCell.setSurvival();
        assert.equal(myCell.willLive, true);
    })

});


describe('Living', function() {
    it('world exists', function() {
        assert(World);
    });
});


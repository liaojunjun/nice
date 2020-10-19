```scss
.flex {
  display: flex;
  &.inline {
    display: inline-flex;
  }
  &.start {
    justify-content: flex-start;
  }
  &._start {
    align-items: flex-start;
  }
  &.center {
    justify-content: center;
  }
  &._center {
    align-items: center;
  }
  &.end {
    justify-content: flex-end;
  }
  &._end {
    align-items: flex-end;
  }
  &.between {
    justify-content: space-between;
  }
  &.around {
    justify-content: space-around;
  }
  &.baseline {
    align-items: baseline;
  }
  &.stretch {
    align-items: stretch;
  }
  &.row {
    flex-direction: row;
  }
  &.row_reverse {
    flex-direction: row-reverse;
    -webkit-box-pack: end;
  }
  &.column {
    flex-direction: column;
  }
  &.column_reverse {
    flex-direction: column-reverse;
    -webkit-box-pack: end;
  }
  &.wrap {
    -ms-flex-wrap: wrap;
    flex-wrap: wrap;
  }
  .child_0 {
    flex-grow: 0;
    flex-shrink: 0;
    display: block;
  }

  .child_1 {
    flex-grow: 1;
    flex-shrink: 1;
    display: block;
  }
  &.dir_row,
  &.dir_row_reverse {
    > .child_0 {
      width: auto;
    }

    > .child_1 {
      width: 0%;
      height: auto;
    }
  }
  &.dir_column,
  &.dir_column_reverse {
    > .child_0 {
      height: auto;
    }

    > .child_1 {
      width: auto;
      height: 0;
    }
  }
}
```

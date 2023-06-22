# Important considerations

## Cells are structures
In csharp structures are passed by value, and not by reference. This means the following code will **NOT** do anything. See the [C# reference](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/struct) for more information.
```csharp
var targetCell = _cellGrid.GetCell(target);
//Both targetCell and targetCell.Transform are structures, meaning this code won't do anything.
targetCell.Value.Transform.Position = new Vector2Int(0, 0);
```

### Updating Cell Position
To update a cell and replace it in the cell grid first remove the cell you want to edit, then add it back with it's updated properties.
```csharp
cellGrid.RemoveCell(cell);
//Update cell transform without loosing cell direction
cell.Transform = cell.Transform.SetPosition(new Vector2Int(0, 0));
cellGrid.AddCell(cell);
```

alternatively, you can use `cellGrid.MoveCell(cell, target);` for a much simpler implementation.
```csharp
//equivalent to previous example
_cellGrid.MoveCell(useCell, target);
```

### Updating Cell Rotation
To update a cell and replace it in the cell grid first remove the cell you want to edit, then add it back with it's updated properties.
```csharp
cellGrid.RemoveCell(cell);
//Update cell transform without loosing cell direction
cell.Transform = cell.Transform.SetDirection(Direction.Up);
cellGrid.AddCell(cell);
```

alternatively, you can use `cellGrid.MoveCell(cell, target);` for a much simpler implementation.
```csharp
//equivalent to previous example
_cellGrid.RotateCell(useCell, newRotation);
```

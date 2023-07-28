# to-path-tree

<a href="https://www.npmjs.com/package/to-path-tree" target="_blank" rel="noopener noreferrer"><img src="https://badgen.net/npm/v/to-path-tree" alt="NPM Version" /></a>
<a href="https://www.npmjs.com/package/to-path-tree" target="_blank" rel="noopener noreferrer"><img src="https://badgen.net/npm/dt/to-path-tree" alt="NPM Downloads" /></a>
<a href="https://github.com/alexzhang1030/to-path-tree/blob/main/LICENSE" target="_blank" rel="noopener noreferrer"><img src="https://badgen.net/github/license/alexzhang1030/to-path-tree" alt="License" /></a>

Convert a file path array to a tree.

## Installation

```bash
pnpm i to-path-tree
```

## Usage

```ts
import { pathToTree } from 'to-path-tree'

const paths = [
  'src',
  'src/index.ts',
  'src/index.test.ts',
  'src/utils',
  'src/utils/index.ts',
  'src/utils/index.test.ts',
  'src/utils/other.ts',
  'src/utils/other.test.ts',
]

const tree = pathToTree(paths)
```

The data structure of the tree is as follows:

```ts
export interface NodeItem<T> {
  path: string
  filename: string
  ext: string
  data?: T
  isEntry: boolean // the entry is index
}

export interface TreeNode<T> {
  items: NodeItem<T>[]
  subDirectory: {
    [key: string]: TreeNode<T>
  } | null
  parent?: TreeNode<T>
}
```

You can use `walkPathTree` to traverse the tree.

For example:

```ts
import { pathToTree, walkPathTree } from 'to-path-tree'

const tree = pathToTree(input)
walkPathTree(tree, (node) => {
  for (const item of node.items) {
    if (item.path === 'src/a/b/d/index.ts') {
      // do something...
    }
  }
})
```

## License

MIT

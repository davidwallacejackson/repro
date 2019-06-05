## Steps

https://asciinema.org/a/xQL4Oo3KQEHKMRVOhgTfy2kFD

```sh
git clone https://github.com/aleclarson/repro.git -b dts-2 dts-2
cd dts-2
yarn
```

### `index.d.ts`

The bundle generated by `dts-bundle-generator`

### `lib/index.d.ts`

The typedefs generated by `tsc`

### Example output

```sh
$ yarn

yarn install v1.15.2
[1/4] 🔍  Resolving packages...
success Already up-to-date.
$ sh prepare.sh
warning package.json: No license field
warning @foo/bar@1.0.0: No license field
[--] 0/2
warning package.json: No license field
warning foo@1.0.0: No license field
[---------------------------------------------------------------------] 0/112
yarn run v1.15.2
warning package.json: No license field
$ tsc -d -p . --outDir lib
✨  Done in 1.16s.


import { Bar } from 'bar';
export declare type Foo = (bar: Bar) => void;
export declare const foo: Foo;
export { bar } from 'bar';


yarn run v1.15.2
warning package.json: No license field
$ dts-bundle-generator -o index.d.ts index.ts
Compiling input files...
WARNING: It seems that some files in the compilation still are not declaration files.
For more information see https://github.com/timocov/dts-bundle-generator/issues/53.
If you think this is a mistake, feel free to open new issue or just ignore this warning.
  /Users/alec/dev/sandbox/repro/foo/node_modules/@foo/bar/index.ts

Processing index.ts
Adding import with name "Bar" for library "@foo/bar"
Writing index.ts -> index.d.ts
Checking generated files...
Done in 2.12s
✨  Done in 2.50s.


import { Bar } from '@foo/bar';

export declare type Foo = (bar: Bar) => void;
export declare const foo: Foo;
export { bar } from 'bar';

export {};


✨  Done in 4.93s.
```

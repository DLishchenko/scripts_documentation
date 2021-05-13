# Файловые системы

1. Локальная файловая система
1. FTP
1. Shared folder
1. Файлы CSV


### Интерфейс Filesystems ...<a name="Filesystems"></a>
```ts
interface Filesystems {
    ftp(): FTPAdapter;
    local(): Filesystem;
    sharedFolder(id: string): Filesystem;
    filesDataManager(): FilesDataManager;
}
```

&nbsp;

```js
ftp(): FTPAdapter
```
Возвращает ссылку на интерфейс [`FTPAdapter`](#FTPAdapter) доступа к FTP.

&nbsp;

```js
local(): Filesystem
```
Возвращает ссылку на интерфейс [`Filesystem`](#Filesystem) доступа к локальной файловой системе.

&nbsp;

```js
sharedFolder(id: string): Filesystem
```

```js
filesDataManager(): FilesDataManager
```

### Интерфейс FileMeta ...<a name="FileMeta"></a>
```ts
interface FileMeta {
    type: string;
    path: string;
    visibility: string;
    size: number;
    dirname: string;
    basename: string;
    extension: string;
    filename: string;
    timestamp: number;
}
```
Интерфейс содержит набор свойств файла или папки.

&nbsp;

```js
type: string
```
Тип объекта: `file` или `dir`.

&nbsp;

`path: string`
Путь к объекту в рабочей п.   ...................

&nbsp;

```js
visibility: string
```

&nbsp;

```js
size: number
```
У файла: размер в байтах. У папок поле отсутствует.

&nbsp;

```js
dirname: string
```
Папка, в которой находится объект. Для объектов в ...... это пустая строка.

&nbsp;

```js
basename: string
```
Имя объекта.

&nbsp;

```js
extension: string
```
Расширение имени без точки. Если расширения нет, поле отсутствует.

&nbsp;

```js
filename: string
```
Имя объекта (файла или папки) без последней точки и расширения.

&nbsp;

```js
timestamp: number
```
Время 

### Интерфейс Filesystem ...<a name="Filesystem"></a>
```ts
interface Filesystem {
    has(path: string): boolean;
    read(path: string): string;
    readAndDelete(path: string): string;
    write(path: string, contents: string): boolean;
    delete(path: string): boolean;
    rename(from: string, to: string): boolean;
    copy(from: string, to: string): boolean;
    getTimestamp(path: string): string;
    getSize(path: string): number;
    createDir(path: string): boolean;
    deleteDir(path: string): boolean;
    listContents(path: string, recursive: boolean): Array<FileMeta>;
    getMetadata(path: string): object;
    upload(from: string, to: string): boolean;
    download(from: string, to: string): boolean;
    makeGlobalFile(name: string, extension: string, path: string, copy?: boolean): string;
    getPathObj(path: string): PathObj;
}
```
Абстрактный интерфейс файловой системы.

&nbsp;

```js
has(path: string): boolean
```
Возвращает признак существования файла/папки по адресу `path`.

&nbsp;

```js
read(path: string): string
```

&nbsp;

```js
readAndDelete(path: string): string
```

&nbsp;

```js
write(path: string, contents: string): boolean
```

&nbsp;

```js
delete(path: string): boolean
```

&nbsp;

```js
rename(from: string, to: string): boolean
```

&nbsp;

```js
copy(from: string, to: string): boolean
```

&nbsp;

```js
getTimestamp(path: string): string
```

&nbsp;

```js
getSize(path: string): number
```

&nbsp;

```js
createDir(path: string): boolean
```
Создаёт папку `path`; при необходимости создаёт промежуточные папки. Возвращает признак успешного выполнения.

&nbsp;

```js
deleteDir(path: string): boolean
```

&nbsp;

```js
listContents(path: string, recursive: boolean): Array<FileMeta>
```

&nbsp;

```js
getMetadata(path: string): object
```

```js
upload(from: string, to: string): boolean
```

&nbsp;

```js
download(from: string, to: string): boolean
```

&nbsp;

```js
makeGlobalFile(name: string, extension: string, path: string, copy?: boolean): string
```

&nbsp;

```js
getPathObj(path: string): PathObj
```


## Локальная файловая система

Локальная файловая система — временная папка на сервере, которая является рабочей директорией скрипта. Скрипт ***НЕ*** может выйти за её пределы.

## FTP

### Интерфейс BaseAdapter<a name="BaseAdapter"></a>
```ts
interface BaseAdapter {
    load(): Filesystem;
}
```
Базовый интерфейс адаптеров файловых систем.

&nbsp;

```js
load(): Filesystem
```
Возвращает объект файловой системы [`Filesystem`](#Filesystem) с предварительно установленными настройками.

### Интерфейс FTPAdapter<a name="FTPAdapter"></a>
```ts
interface FTPAdapter extends BaseAdapter {
    setHost(host: string): FTPAdapter;
    getHost(): string;

    setPort(port: number): FTPAdapter;
    getPort(): number;

    setUsername(username: string): FTPAdapter;
    getUsername(): string;

    setPassword(password: string): FTPAdapter;
    getPassword(): string;

    setRoot(root: string): FTPAdapter;
    getRoot(): string;

    setPassive(passive: boolean): FTPAdapter;
    getPassive(): boolean;

    setSsl(ssl: boolean): FTPAdapter;
    getSsl(): boolean;

    setTimeout(timeout: number): FTPAdapter;
    getTimeout(): number;

    setUseListOptions(useListOptions: boolean): FTPAdapter;
    getUseListOptions(): boolean;
}
```

Интерфейс, реализующий шаблон проектирования [`строитель`](https://ru.wikipedia.org/wiki/%D0%A1%D1%82%D1%80%D0%BE%D0%B8%D1%82%D0%B5%D0%BB%D1%8C_(%D1%88%D0%B0%D0%B1%D0%BB%D0%BE%D0%BD_%D0%BF%D1%80%D0%BE%D0%B5%D0%BA%D1%82%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D1%8F)), для соединения с сервером [`FTP`](https://ru.wikipedia.org/wiki/FTP).

&nbsp;

```js
setHost(host: string): FTPAdapter
```
Устанавливает адрес хоста. Возвращает `this`.

&nbsp;

```js
getHost(): string
```
Возвращает адрес хоста.

&nbsp;

```js
setPort(port: number): FTPAdapter
```
Устанавливает номер порта. Возвращает `this`.

&nbsp;

```js
getPort(): number
```
Возвращает номер порта.

&nbsp;

```js
setUsername(username: string): FTPAdapter
```
Устанавливает имя пользователя. Возвращает `this`.

&nbsp;

```js
getUsername(): string
```
Возвращает имя пользователя.

&nbsp;

```js
setPassword(password: string): FTPAdapter
```
Устанавливает пароль. Возвращает `this`.

&nbsp;

```js
getPassword(): string
```
Возвращает пароль.

&nbsp;

```js
setRoot(root: string): FTPAdapter
```
Устанавливает начальный путь для работы с FTP. По умолчанию: `/`. Возвращает `this`.

&nbsp;

```js
getRoot(): string
```
Возвращает начальный путь для работы с FTP.

&nbsp;

```js
setPassive(passive: boolean): FTPAdapter
```
Устанавливает активный или пассивный режим соединения. По умолчанию: `true`. Возвращает `this`.

&nbsp;

```js
getPassive(): boolean
```
Возвращает признак пассивности режима соединения.

&nbsp;

```js
setSsl(ssl: boolean): FTPAdapter
```
Устанавливает признак использования протокола [`SSL`](https://ru.wikipedia.org/wiki/SSL) поверх FTP ([`FTPS`](https://ru.wikipedia.org/wiki/FTPS)). По умолчанию: `false`. Возвращает `this`.

&nbsp;

```js
getSsl(): boolean
```
Возвращает признак использования протокола SSL.

&nbsp;

```js
setTimeout(timeout: number): FTPAdapter
```
Устанавливает таймаут подключения к серверу в секундах. По умолчанию: `30`. Возвращает `this`.

&nbsp;

```js
getTimeout(): number
```
Возвращает таймаут подключения к серверу в секундах.

&nbsp;

```js
setUseListOptions(useListOptions: boolean): FTPAdapter
```
Устанавливает флаги `-aln` у FTP-команды `LIST`. FTP может быть настроен по особенному, поэтому иногда требуется передать `false`. По умолчанию: `true`. Возвращает `this`.

&nbsp;

```js
getUseListOptions(): boolean
```
Возвращает признак использованися флагов `-aln` у FTP-команды `LIST`.

## Shared folder


## Файлы CSV



[API Reference](API.md)

[Оглавление](../README.md)
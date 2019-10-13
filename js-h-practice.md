## 函数封装歌曲管理
### 增
	

```
	function addSong(song){
//            songList.push(song);
//        }
//
//        addSong({
//            songName:"take me to your heart",
//            singer:"迈克学摇滚"
//        });
```


#### 删
	

```
	function removeSong(songName){
            var song = selectSong(songName);
            var index = songList.indexOf(song);
            songList.splice(index, 1);

//            for (var i = 0; i < songList.length; i++) {
//                var song = songList[i];
//                if(song.songName == songName){
//                    //splice(起始索引,删几个)
//                    songList.splice(i, 1);
//                }
//            }
        }

        removeSong("李白");
```


### 改
	

```
	 function updateSong(songName, singer) {

            var song = selectSong(songName);
            song.singer = singer;

            //遍历歌曲列表，找到要修改的对象
//            for (var j = 0; j < songList.length; j++) {
//                var song = songList[j];
//                //判断每次遍历的对象的歌名，和要找的歌名是不是一一致，如果一致，就是我们要找的对象
//                if(song.songName == songName){
//                    //对找到的对象进行修改
//                    song.singer = singer;
//                }
//            }
        }
//
//        updateSong("演员","薛之谦");
//        console.log(songList);
```

### 查
	

```
	function selectSong(songName) {
            for (var k = 0; k < songList.length; k++) {
                var song = songList[k];
                if(song.songName == songName){
                    return song;
                }
            }
            return null;
        }
```
## 面向对象封装歌曲管理
在当前对象的方法中，调用当前对象的其他方法，需要使用this
例如 在 removeSong方法中调用 selectSong  this.selectSong
	

```
function SongManager(){
            this.songList = null;
        }
 
SongManager.prototype = {
            init:function (songList) {
                this.songList = songList;
            },

            addSong: function (song){
                this.songList.push(song);
            },

            removeSong:function (songName){
                var song = this.selectSong(songName);
                if(song == null){
                    throw "您要删除的歌曲不存在！请重新尝试";
                }
                var index = this.songList.indexOf(song);
                this.songList.splice(index, 1);
            },

            updateSong: function (songName, singer) {
                var song = this.selectSong(songName);
                if(song == null){
                    throw "您要修改的歌曲不存在！请重新尝试";
                }
                song.singer = singer;
            },

            selectSong: function (songName) {
                for (var k = 0; k < this.songList.length; k++) {
                    var song = this.songList[k];
                    if(song.songName == songName){
                        return song;
                    }
                }
                return null;
            }
        };
	调用
 var pwbDEManager = new SongManager();
        pwbDEManager.init([
            {
                songName:"青藏高原",
                singer:"潘文斌"
            },
            {
                songName:"我的换板鞋，摩擦摩擦最时尚",
                singer:"约翰逊，庞麦郎"
            }
        ]);
gjbDEManager.removeSong("两只老虎");
```


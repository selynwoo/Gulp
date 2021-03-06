#Javascript 명령어 
- `gulp-concat` (병합)
- `gulp-uglify` (압축)
- `gulp-jshint` (문법검사)
- `gulp-rename` (압축, 비압축 파일 출력)
- `del` (특정 디렉터리 및 파일 삭제)

<br>
## gulp-concat (병합) 
- **설치 [ cmd : `npm i -D gulp-concat` ]**

- **Modules 호출**
```md
var gulp = require('gulp'),
    concat = require('gulp-concat');
```

- **지정한 js 병합** <br>
```md
gulp.task('combine:js', function(){
	gulp
		.src(['./src/domheler-id.js', './src/domheler-tag.js'])
		.pipe(concat('combined.js'))
		.pipe(gulp.dest('./dist'));
});
```

- **모든 js 병합** <br>
```md
gulp.task('combine:js', function(){
	gulp
		.src('./src/*.js') 
		.pipe(concat('combined.js'))
		.pipe(gulp.dest('./dist'));
});
```

- **특정파일 우선적 병합** <br>
```md
gulp.task('combine:js', function(){
	gulp
		.src(['./src/domhelper-prevEl.js', './src/*.js']) 
		.pipe(concat('combined.js'))
		.pipe(gulp.dest('./dist'));
});
```

- **하위디렉터리 모든 js 병합** <br>
```md
gulp.task('combine:js', function(){
	gulp
		.src('src/js/libs/**/*.js') //src 디렉터리의 js/libs 하위 디렉터리를 생성 후 실행 후 확인
		.pipe(concat('combined.js'))
		.pipe(gulp.dest('./dist'));
});
```
<br>
## gulp-uglify (압축) 
- **설치 [ cmd : `npm i -D gulp-uglify` ]**

- **Modules 호출**
```md
var gulp = require('gulp'),
    uglify = require('gulp-uglify'),
    concat = require('gulp-concat');
```

- **압축** <br>
```md
gulp.task('combine:js', function(){
	gulp
		.src('src/js/libs/**/*.js')
		.pipe(concat('combined.js'))
		.pipe(uglify())
		.pipe(gulp.dest('./dist'));
});
```

- **압축 조건** <br>
```md
gulp.task('combine:js', function(){
	gulp
		.src('src/js/libs/**/*.js')
		.pipe(concat('combined.js'))
		.pipe(uglify({
			mangle : false, //변수, 매개변수 축약여부
			preserveComments: 'all' // 'all' : 모든주석 보존, 'some' : !(느낌표)가 붙은 주석만 보존
		}))
		.pipe(gulp.dest('./dist'));
});
```
<br>
## gulp-jshint (문법검사) 
- **설치 [ cmd : `npm i -D gulp-jshint` ]**
- **설치 [ cmd : `npm i jshint-stylish` ]**
- **문법검사는 js 병합전**

- **Modules 호출**
```md
var gulp = require('gulp'),
    jshint = require('gulp-jshint'),
    uglify = require('gulp-uglify'),
    concat = require('gulp-concat');
```
- **일반** <br>
```md
gulp.task('combine:js', function(){
	gulp
		.src('src/js/libs/**/*.js')
		.pipe(jshint())
		.pipe(concat('combined.js'))
		.pipe(uglify({
			mangle : false,
			preserveComments: 'all'
		}))
		.pipe(gulp.dest('./dist'));
});
```

- **가독성** <br>
```md
gulp.task('combine:js', function(){
	gulp
		.src('src/js/libs/**/*.js')
		.pipe(jshint())
		.pipe(jshint.reporter('jshint-stylish'))
		.pipe(concat('DOMLibrary.js'))
		.pipe(uglify({
			mangle : false,
			preserveComments: 'all'
		}))
		.pipe(gulp.dest('./dist'));
});
```
<br>
## gulp-rename (압축, 비압축 파일 출력) 
- **설치 [ cmd : `npm i -D gulp-rename` ]**

- **Modules 호출**
```md
var gulp = require('gulp'),
    jshint = require('gulp-jshint'),
    uglify = require('gulp-uglify'),
    concat = require('gulp-concat'),
    rename = require('gulp-rename');
```

- **압축, 비압축 파일 출력** <br>
```md
gulp.task('combine:js', function(){
	gulp
		.src('src/js/libs/**/*.js')
		.pipe(jshint())
		.pipe(jshint.reporter('jshint-stylish'))
		.pipe(concat('DOMLibrary.js')) //비압축
		.pipe(gulp.dest('./dist'))
		.pipe(uglify({
			mangle : false,
			preserveComments: 'all'
		}))
		.pipe(rename('DOMLibrary.min.js')) //압축
		.pipe(gulp.dest('./dist'));
});
```
<br>
## del (특정 디렉터리 및 파일 삭제) 
- **설치 [ cmd : `npm i -D del` ]**

- **Modules 호출**
```md
var gulp = require('gulp'),
    jshint = require('gulp-jshint'),
    uglify = require('gulp-uglify'),
    concat = require('gulp-concat'),
    rename = require('gulp-rename'),
    del = require('del');
```
- **테스크 정의** <br>
```md
gulp.task('clean', function(){
	del(['dist/*']);
	del(['dist/*', '!dist/dont-delete.js']); //느낌표(!)를 붙이면 삭제대상에서 제외된다.
});
 
```
<br>
## 기본(Default) 테스크 정의
- script 업무 
 + 파일문법검사 > 병합 > 압축
 + gulp.task('scripts', ['js:hint', 'js:concat', 'js:uglify']);
 
- clean 업무 
 + script 업무 이전에 clean 업무가 실행되도록 설정하여 저장.
 + gulp.task('default', ['clean', 'scripts']); 
 
 **테스크 정의**
 ```md
var path = {
	js: {
		src: 'src/js/libs/**/*.js',
		dest: 'dist/',
		filename: 'DOMLibrary.js'
	}
};

// JS 문법검사
gulp.task('js:hint', function(){
	gulp.src(path.js.src)
		.pipe(jshint())
		.pipe(jshint.reporter('jshint-stylish'));
});

// JS 병합
gulp.task('js:concat', function(){
	gulp.src(path.js.src)
		.pipe(concat(path.js.filename))
		.pipe(gulp.dest(path.js.dest));
});

// JS 압축
gulp.task('js:uglify', function(){
	gulp.src(path.js.dest + path.js.filename)
		.pipe(uglify())
		.pipe(rename( { suffix: 'min' } )) //접미사 min
		.pipe(gulp.dest(path.js.dest));
});

gulp.task('clean', function(){
	del(['dist/*']);
	del(['dist/*', '!dist/dont-delete.js']); //느낌표(!)를 붙이면 삭제대상에서 제외된다.
});
 ```
 
 

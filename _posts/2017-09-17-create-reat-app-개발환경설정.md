---
    layout: post
---
### 1. 프로젝트 생성
`create-react-app 프로젝트이름`

### 2. react-scripts 제거
webpack 설정을 customizing 하기 위해 실행합니다.

`npm run eject`

### 3. Include 미디어 설치

반응형 layout을 쉽게 만들 수 있게 해주는 library.

`yarn add include-media`

### 4. Open color 설치
color선택을 도와주는 library.
`yarn add open-color`

### 5. ImmutableJs 설치
`yarn add immutable`

### 6. Lodash 설치
`yarn add lodash`

### 7. Sass loader 설치 및 설정
`yarn add --dev node-sass sass-loader`

- loader 설정: 아래 코드를 webpack.config.dev.js 및 webpack.config.prod.js의 css loader 다음에 넣습니다.

```javascript
          {
            test: /\.scss$/,
            use: [
              require.resolve('style-loader'),
              {
                loader: require.resolve('css-loader'),
                options: {
                  importLoaders: 1,
                },
              },
              {
                loader: require.resolve('postcss-loader'),
                options: {
                  // Necessary for external CSS imports to work
                  // https://github.com/facebookincubator/create-react-app/issues/2677
                  ident: 'postcss',
                  plugins: () => [
                    require('postcss-flexbugs-fixes'),
                    autoprefixer({
                      browsers: [
                        '>1%',
                        'last 4 versions',
                        'Firefox ESR',
                        'not ie < 9', // React doesn't support IE8 anyway
                      ],
                      flexbox: 'no-2009',
                    }),
                  ],
                },
              },
              {
                loader: require.resolve('sass-loader'),
              }
            ],
          },
```

- main style path 설정: paths.js의 module.exports 객체에 아래 코드를 추가 합니다. (src/styles/main.scss를 생성해야 합니다.)

`appMainStyle: resolveApp('src/styles/main.scss'),`

- webpack.config.dev.js의 entry배열에 main style path 추가 합니다.

`paths.appMainStyle`

### 8. redux, redux-actions, react-redux 설치

`yarn add redux redux-actions react-redux`

### 9. react-onclickoutside 설치
모듈, dropdown 같은 컴포넌트를 만들때 사용합니다.

`yarn add redux-onclickoutside`

### 10. react-router 설치

`yarn add react-router@3.0.5`
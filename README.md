# Feature Focus React Architecture

🔥 ⚛️ A feature focus architecture for building scalable, powerful, and production ready React Applications.

## Introduction

Despite how amazing React is, there are no specific conventions or best practices regarding architecturing production grade React application. The usual advice is to just start programming and later move files [until it feels right](https://react-file-structure.surge.sh/). Basically to not concern ourselves with the file structure for our React app when starting out with React.

Unfortunately, for teams/people that are working on serious applications,this kind of advice is not that helpful since trial & error would end up costing a lot of money and time in the process. What they actually need are a clear and opiniated way to organize their files (i.e. app architecture) as a guidance. So that they can move fast delivering features, without getting stuck forever on deciding what kind of architecture they should use.

After several years working with React and having the same frustration, I decided to open source my own React app architecture which I called a `Feature Focus React Architecture`. This is not a perfect architecture. This is also not a Clean Architecture, the kind of architecture that is used heavily in most backend applications. But I think, this architecture serves the need to provide a nice separation of concerns and also for quickly delivering feature on the Frontend application with React.

These architecture are not entirely created by myself. I have combined and adjusted the file structure from multiple inspirations. From the architecture that is used at my work, and also from several articles as follows:

- React Architecture: How to Structure and Organize a React Application: https://www.taniarascia.com/react-architecture-directory-structure/
- Bulletproof React: https://github.com/alan2207/bulletproof-react
- Micro-app folder/file hierarchy: https://www.cantankerouscoder.com/p/micro-app-folderfile-hierarchy

Again, the purpose of this architecture is not to implement a perfect and clean architecture for the frontend. The only goal of this architecture is to help people to focus more on delivering features quickly, timely, and as scalable as possible.

A little caveat. This architecture currently is not designed to handle monorepo projects. But you can easily use this as a basis to configure monorepo architecture for your own project.

<hr>

## Tech Stacks

The recommended tech stacks to use if you want to adopt this architecture are as follows:

- Build Tool - Vite
- Application - React, React Hooks
- Global state management - Redux, Redux Toolkit (RTK)
- API Integration - Redux Toolkit Query (RTK Query)
- Routing - React Router
- Styles - TailwindCSS, twin.macro
- Testing - Jest, React Testing Library, React Hooks Testing Library
- Code Formatting - Eslint & Prettier
- Commit Structure: Conventional Commit, Husky

I will explain reasoning for each choices later.

<hr>

## App Architecture

This is what I came up with for the **Feature Focus React Architecture**. I have also included some file examples on each directory.

```text
.
└── src/
    ├── app/
    │   ├── container/
    │   │     ├── App.tsx
    │   │     ├── App.test.tsx
    │   │     ├── ErrorBoundary.app.tsx
    │   │     ├── ErrorBoundary.app.test.tsx
    │   │     ├── GlobalStyles.app.tsx
    │   │     └── GlobalStyles.app.test.tsx
    │   │
    │   └── store/
    │         ├── store.app.tsx
    │         └── store.app.test.tsx
    ├── assets/
    │   ├── images/
    │   └── index.ts
    │
    ├── shared/
    │   ├── models/
    │   │   ├── Auth.model.ts
    │   │   └── AnotherSharedModel.model.ts
    │   │
    │   ├── components/
    │   │   ├── Icons/
    │   │   │   ├── IconA.tsx
    │   │   │   ├── IconB.tsx
    │   │   │   └── index.ts
    │   │   └── CardContainer/
    │   │	      ├── CardContainer.tsx
    │   │	      ├── CardContainer.test.tsx
    │   │	      └── CardContainer.stories.tsx
    │   │
    │   ├── hooks/
    │   │   └── useTranslator/
    │   │       ├── useTranslator.hook.ts
    │   │       └── useTranslator.hook.test.ts
    │   │
    │   ├──	utils/
    │   │	   ├── dateFormatter/
    │   │	   │	  ├── dateFormatter.util.ts
    │   │	   │	  └── dateFormatter.util.test.ts
    │   │	   └── toCamelCase/
    │   │		       ├── toCamelCase.util.ts
    │   │		       └── toCamelCase.util.test.ts
    │   │
    │   └── constants/
    │    	  ├── someConstant.constant.ts
    │    	  └── anotherConstant.constant.ts
    │
    ├── configs/
    │   ├── env/
    │   │	  ├── env.config.ts
    │   │	  └── env.config.test.ts
    │   │
    │   ├── router/
    │   │	  ├── router.config.ts
    │   │	  └── router.config.test.ts
    │   │
    │   └── persist/
    │       ├── persist.config.ts
    │       └── persist.config.test.ts
    │
    ├── store/
    │   ├── slices/
    │   │   ├── authentication
    │   │   │   ├── authentication.slice.ts
    │   │   │   └── authentication.slice.test.ts
    │   │   │
    │   │   └── order
    │   │       ├── order.slice.ts
    │   │       └── order.slice.test.ts
    │   │
    │   ├── rootReducer.store.ts
    │   └── index.ts
    │
    ├── route/
    │	  ├── routeList.route.ts
    │	  ├── AppRouter.route.ts
    │	  └── AppRouter.route.test.ts
    │
    ├── services/
    │   ├── storage/
    │   │   ├── adapters/
    │   │   │   ├── storage.type.ts
    │   │   │   │
    │   |   │   ├── localStorage/
    │   │   │   │    ├── localStorage.adapter.ts
    │   │   │   │    └── localStorage.adapter.test.ts
    │   │   │   │
    │   │   │   └── localForage/
    │   │   │        ├── localForage.adapter.ts
    │   │   │        └── localForage.adapter.test.ts
    │   │   │
    │   │   ├── storage.service.ts
    │   │   └── storage.service.test.ts
    │   │
    │   └── monitoring/
    │       ├── adapters/
    │       │   ├── monitoring.type.ts
    │       │   │
    │       │   └── sentry/
    │       │       ├── sentry.adapter.ts
    │       │       └── sentry.adapter.test.ts
    │       │
    │       ├── monitoring.service.ts
    │       └── monitoring.service.test.ts
    │
    └── api/
    │   ├── endpoints/
    │   │   │
    │   │   ├── auth/
    │   │   │   ├── auth.endpoint.ts
    │   │   │   └── auth.endpoint.test.ts
    │   │   ├── product/
    │   │   │   ├── product.endpoint.ts
    │   │   │   └── product.endpoint.test.ts
    │   │   └── profile/
    │   │       ├── profile.endpoint.ts
    │   │       └── profile.endpoint.test.ts
    │   │
    │   ├── api.baseQuery.ts
    │   └── api.service.ts
    │
    ├── features/
    │   ├── Product/
    │   │	  ├── components/
    │   │	  │    ├── ProductListTable
    │   │	  │	   │    ├── ProductListTable.tsx
    │   │	  │	   │    ├── ProductListTable.test.tsx
    │   │	  │	   │    └── ProductListTable.stories.tsx
    │   │	  │    └── CreateProductForm
    │   │	  │	        ├── CreateProductForm.tsx
    │   │	  │	        ├── CreateProductForm.test.tsx
    │   │	  │	        └── CreateProductForm.stories.tsx
    │   │	  ├── util/
    │   │	  │    └── someUtil/
    │   │	  │        ├── someUtil.util.ts
    │   │	  │        └── someUtil.util.test.ts
    │   │	  ├── model/
    │   │	  │    ├── Products.model.ts
    │   │	  │    └── Discount.model.ts
    │   │	  ├── hooks/
    │   │	  │    └── useCreateProductForm
    │   │	  │        ├── useCreateProductForm.hook.ts
    │   │	  │        └── useCreateProductForm.hook.test.ts
    │   │	  └── views/
    │   │	       ├── CreateProduct/
    │   │	       │   ├── CreateProduct.view.tsx
    │   │	       │   ├── CreateProduct.view.test.tsx
    │   │	       │   ├── CreateProduct.viewModel.tsx
    │   │	       │   ├── CreateProduct.viewModel.test.tsx
    │   │	       │   ├── CreateProduct.route.tsx
    │   │	       │   └── CreateProduct.test.tsx
    │   │	       └── ProductList/
    │   │	           ├── ProductList.view.tsx
    │   │	           ├── ProductList.view.test.tsx
    │   │	           ├── ProductList.viewModel.tsx
    │   │	           ├── ProductList.viewModel.test.tsx
    │   │	           ├── ProductList.route.tsx
    │   │	           ├── ProductList.test.tsx
    │   │	           └── views/
    │   │	                 ├── BestSellerTab
    │   │	                 └── RecommendebTab
    │   └── auth/
    │       ├── components/
    │       │    ├── SignInForm
    │       │    │	 ├── SignInForm.tsx
    │       │    │   ├── SignInForm.test.tsx
    │       │    │   └── SignInForm.stories.tsx
    │       │    └── SignUpForm
    │       │	 	     └── ....
    │       ├── util/
    │       │    └── form/
    │       │        ├── form.util.ts
    │       │        └── form.util.test.ts
    │       └── ...
    │
    └── index.tsx
```

Some notes regarding the structure & decision behind it:

- It is better to wrap some utilities function in our own utility functions. This is so that, when there is a breaking changes or error from the 3rd party libraries we are using, we can change the implementations detail later without having to track down usage in multiple files across the codebases.
- Slice is put on the root directory of src since there is a possibility that one redux slices will be used by multiple features.
- Service that uses adapter will implement interface. Therefore we can change internal implementations using different tools & libraries without worrying about breaking changes that will occur.
- Everything that is in the `shared` directory will be shared and used by multiple components, views, and also hooks.
- Everything that is specific to a feature, for example a util function, is designed to be used only for that feature.

<hr>

## TODO List

- [ ] Initiate repo with `vite` & proposed tech stacks
- [ ] Add more explanations about architecture & reason for each tech stack
- [ ] Create example projects. Use `Supabase` for low-code backend to provide REST API

<hr>

## Contributing

Contributions are always welcome! If you have any ideas, suggestions, fixes, feel free to contribute. You can do that by going through the following steps:

Clone this repo
Create a branch: git checkout -b your-feature
Make some changes
Test your changes
Push your branch and open a Pull Request

# FAQ

Here are some answers to common questions. Don't see yours here?
[Open an issue](https://github.com/jmeas/react-request/issues/new) and
we would be happy to help.

#### Why was this created?

While I was studying Apollo, a framework for GraphQL, I learned that its React library exports a
higher-order component that enables a developer to declaratively specify HTTP requests. It surprised me
that this was the primary method that Apollo developers were interfacing with GraphQL over HTTP.

It didn't take long for me to understand that the Apollo HoC was remarkably useful. And although some of the features
that it provides only make sense in the context of GraphQL, I noticed that other features, such as request
deduplication and response caching, would be incredibly useful to any developer who is writing React code.

The only problem is that you can't use Apollo's HoC unless you use GraphQL. This is why I wrote React Request:
to abstract this functionality out into a general-use component.

#### Why would anyone want to use JSX for making HTTP requests?

I was skeptical at first, too, but it turns out that many of the complex things people do with HTTP requests (namely,
request deduplication and response caching) map nicely to the component lifecycle. You can remove a considerable amount
of difficult-to-test imperative code from your application by declaratively specifying how you want your requests to
behave through JSX.

#### If a request is made when the component mounts, how does that work for POST, PATCH, or DELETE requests?

The default behavior is that requests are only made on mount for `GET` requests when the component mounts, and
not for those other HTTP methods.

One of the things that is passed into the render prop function is a method called `fetch`. Calling this method will perform
the request. This allows you to hook up, say, a PATCH request to a button.

Whether or not the request makes a request on mount can be customized with the `lazy` prop.

#### What if I just want a regular fetch component without deduplication or caching features?

Take a look at [Holen](https://github.com/tkh44/holen).

#### What about normalization of data? Apollo does this.

That requires a definition of what a "resource" (or "entity") is, which is a little bit too opinionated for this
library.

With that said, this library is an excellent tool to use to build React bindings for a more opinionated framework
that does define a resource or entity. For instance, the [Redux Resource](https://redux-resource.js.org) React bindings
will be built using React Request.

#### Why isn't this a higher-order component like Apollo's `graphql`?

The render prop pattern is more powerful than Higher Order Components. Read
[this post](https://cdb.reacttraining.com/use-a-render-prop-50de598f11ce) for more.

In an upcoming version of React Apollo, they, too, will export render prop components.

#### Why is the prop named `children` rather than `render`?

Although there are a handful of arguments for the render prop to be `render` rather than `children`, this library is
using the same pattern that React's [new Context API](https://github.com/reactjs/rfcs/pull/2) uses.

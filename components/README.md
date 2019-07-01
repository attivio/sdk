# Components

Attivio makes it easy to create custom components or stages for document, query, and response \(to queries\) processing. The README page provides instructions for using maven archetypes to generate examples. This guide describes the interfaces and general processing architecture for Attivio components.

Components are small chunks of Java code which are executed by the Attivio framework as documents and queries pass through the system. A good component should be focused on a small task \(such as capitalizing text\), keep little to no state, and be designed to be independent of other components in the system. These principles make components reusable in other contexts and composable.

Your component may be created many times \(multiple instances\) within the same Java process. This is used for parallelization purposes and to allow dynamic changes to take place. For this reason, static data, expensive startup/shutdown code, and heavy memory use should be avoided within your components.

{% hint style="info" %}
Components whose instances need to share data should consider using the [`ThreadSafe`](https://github.com/mmasi-attivio/sdk/blob/develop/components/components-writing.md#annotations) annotation.
{% endhint %}


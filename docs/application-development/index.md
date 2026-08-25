!!! info
    Portions of this documentation are adapted from *[OpenHarmony docs](https://gitcode.com/openharmony/docs)* by *OpenHarmony community*, licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).


# Development Overview

## Welcome to Oniro Application Development

Oniro is a modern, flexible operating system designed for diverse device scenarios. This documentation is your starting point for Oniro application development. It provides clear, concise tutorials and practical examples, enabling you to get started quickly without needing to understand all underlying complexities immediately.

By following this documentation, you'll learn how to:

- Set up a straightforward development environment.
- Build and run your first simple Oniro application.
- Gradually master essential concepts to advance your development journey.

## Development Environment
To start developing Oniro applications, you first need to set up the development environment by installing `DevEco Studio`.

For detailed instructions, see the [Environment Setup Guide](environment-setup-guide/index.md).

## Learning Path
To support your application development, we provide comprehensive development guidelines.

You can familiarize yourself with the application development process by [getting started with a simple project](create-first-eclipse-oniro-app/index.md).

## OpenHarmony Version and API Level Reference

Before setting up your development environment, review the relationship between OpenHarmony system versions and their corresponding API levels. This mapping helps you choose the correct API version for your target OpenHarmony system.

<div style="width:100%;box-sizing:border-box; display:flex; justify-content:center;">
  <div style="width:100%; max-width:720px; box-sizing:border-box;">
    <table style="width:100%; table-layout:fixed; border-collapse:separate; border-spacing:0; border:1px solid #e6e6e6; border-radius:6px; overflow:hidden;">
      <thead style="background:#fafafa;">
        <tr>
          <th style="text-align:left;padding:12px 14px;white-space:normal;font-weight:600;border-right:1px solid #f0f0f0;">Version</th>
          <td style="text-align:center;padding:12px 10px;">4.0</td>
          <td style="text-align:center;padding:12px 10px;">4.1</td>
          <td style="text-align:center;padding:12px 10px;">5.0.0</td>
          <td style="text-align:center;padding:12px 10px;">5.0.1</td>
          <td style="text-align:center;padding:12px 10px;">5.0.2</td>
          <td style="text-align:center;padding:12px 10px;">5.0.3</td>
          <td style="text-align:center;padding:12px 10px;">5.1.0</td>
          <td style="text-align:center;padding:12px 10px;">6.0</td>
          <td style="text-align:center;padding:12px 10px;">6.1</td>
        </tr>
      </thead>
      <tbody>
        <tr>
          <th style="text-align:left;padding:12px 14px;white-space:normal;background:#fff;font-weight:600;border-right:1px solid #f0f0f0;">API Level</th>
          <td style="text-align:center;padding:12px 10px;">10</td>
          <td style="text-align:center;padding:12px 10px;">11</td>
          <td style="text-align:center;padding:12px 10px;">12</td>
          <td style="text-align:center;padding:12px 10px;">13</td>
          <td style="text-align:center;padding:12px 10px;">14</td>
          <td style="text-align:center;padding:12px 10px;">15</td>
          <td style="text-align:center;padding:12px 10px;">18</td>
          <td style="text-align:center;padding:12px 10px;">20</td>
          <td style="text-align:center;padding:12px 10px;">23</td>
        </tr>
      </tbody>
    </table>
  </div>
</div>

!!! tip "API Level Selection"
    Select the API level that corresponds to the target OpenHarmony system version. For example, use API level 23 for OpenHarmony 6.1.

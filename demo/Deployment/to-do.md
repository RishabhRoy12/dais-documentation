# To-Do

## Pages still to document

These three pages sit under **Deployment → Owned Channels**. They have no UI document and no Execution document yet.

| Page | Needs | Notes |
|------|-------|-------|
| **Robot.txt** | UI doc and Execution doc | See below |
| **Sitemap** | UI doc and Execution doc | Same as Robot.txt |
| **Internal Linking** | Decision first | The internal team has advised **removing** this page. See below |

---

### Robot.txt

- The page holds data about a brand's **robots.txt** file.
- The data is **not sent monthly**. It is sent **once every few months**, so it does not follow the monthly pattern of the other Deployment pages.
- There is **no approval flow**.
- **Brand users can see** this page on their dashboard.
- A sample CSV exists. The columns are:

| Column | Example in the sample |
|--------|-----------------------|
| `page_url` | `https://www.example.com/` |
| `file_uploaded` | A link to the uploaded file, for example a Google Doc link |
| `file_content` | The robots.txt text, for example `User-agent: *` and `Disallow: /cart` (multi-line text inside quotes) |
| `dias_comments` | A team comment, for example *"Please upload to root"* |
| `status` | For example `Pending` |

### Sitemap

- **Same as Robot.txt**: data sent once every few months, no approval flow, and brand users can see it on their dashboard.
- A sample CSV exists with the **same five columns**: `page_url`, `file_uploaded`, `file_content`, `dias_comments`, `status`. In the sample, `file_content` holds the sitemap XML (for example `<urlset>...</urlset>`), and `dias_comments` and `status` are empty.

### Internal Linking

- The page holds data about **internal linking**.
- It **has an approval flow**.
- The internal team is **not using it** at present and has advised **removing the page**.
- A sample CSV exists. The columns are:

| Column | Example in the sample |
|--------|-----------------------|
| `page_url` | The page where the link is placed |
| `anchor_text` | The link text, for example *best running shoes* |
| `link` | The link on the page. One sample row leaves it empty |
| `interlinking_to` | The page the link should point to |




---
created: <% tp.date.now("YYYY-MM-DD HH:mm") %>
title: <%* tR += moment(tp.file.title, "YYYY-MM-DD").format("YYYY-MM-DD — [Daily Note]"); %>
last-updated: <% tp.date.now("YYYY-MM-DD HH:mm") %>
---
<%*
// Parse date once and reuse
const today = moment(tp.file.title, "YYYY-MM-DD");
const todayFormatted = today.format('YYYY-MM-DD');

// Header: YYYY-MM-DD — Weekday
tR += `\n# ${todayFormatted} — ${today.format('dddd')}\n\n`;

// Breadcrumb navigation
tR += `[[${today.format('YYYY')}]]  /  [[${today.format('YYYY-MM|MMMM')}]]  /  [[${today.format('GGGG-[W]WW|[Week] w')}]]\n`;

// Day navigation
const prevDay = today.clone().subtract(1, 'day');
const nextDay = today.clone().add(1, 'day');
tR += `❮  [[${prevDay.format('YYYY-MM-DD')}]]  |  ${todayFormatted}  |  [[${nextDay.format('YYYY-MM-DD')}]]  ❯\n`;
%>
## Daily Journal Sections

…

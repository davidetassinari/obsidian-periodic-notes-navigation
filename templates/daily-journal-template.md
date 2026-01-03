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

// Breadcrumb navigation with year-spanning logic
const prevDay = today.clone().subtract(1, 'day');
const nextDay = today.clone().add(1, 'day');

// Check if this day bridges two years
const prevYear = prevDay.year();
const currentYear = today.year();
const nextYear = nextDay.year();

let breadcrumb = `[[${today.format('YYYY')}]]  /  [[${today.format('YYYY-MM|MMMM')}]]  /  [[${today.format('GGGG-[W]WW|[Week] W')}]]`;

// If previous day is in a different year (Jan 1)
if (prevYear !== currentYear) {
    breadcrumb = `[[${prevYear}]]  –  [[${currentYear}]]  /  [[${prevDay.format('YYYY-MM|MMMM')}]]  –  [[${today.format('YYYY-MM|MMMM')}]]  /  [[${today.format('GGGG-[W]WW|[Week] W')}]]`;
}
// If next day is in a different year (Dec 31)
else if (nextYear !== currentYear) {
    breadcrumb = `[[${currentYear}]]  –  [[${nextYear}]]  /  [[${today.format('YYYY-MM|MMMM')}]]  –  [[${nextDay.format('YYYY-MM|MMMM')}]]  /  [[${today.format('GGGG-[W]WW|[Week] W')}]]`;
}

tR += breadcrumb + '\n';

// Day navigation
tR += `❮  [[${prevDay.format('YYYY-MM-DD')}]]  |  ${todayFormatted}  |  [[${nextDay.format('YYYY-MM-DD')}]]  ❯\n`;
%>
## Daily Journal Sections

…

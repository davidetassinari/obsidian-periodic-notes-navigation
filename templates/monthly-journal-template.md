---
created: <% tp.date.now("YYYY-MM-DD HH:mm") %>
title: <%* const titleMoment = moment(tp.file.title, "YYYY-MM"); tR += titleMoment.format("YYYY-MM") + " — Monthly Note"; %>
last-updated: <% tp.date.now("YYYY-MM-DD HH:mm") %>
---
<%*
const month = moment(tp.file.title, "YYYY-MM");
const monthPath = month.format('MM-MMMM');
const monthYear = month.format('MMMM YYYY');

// Header
tR += `\n# ${monthYear}\n\n`;

// Navigation: changed for January and December
const prevMonth = month.clone().subtract(1, "month");
const nextMonth = month.clone().add(1, "month");
const currentYear = month.format("YYYY");
const prevYear = prevMonth.format("YYYY");
const nextYear = nextMonth.format("YYYY");

// Start with current year (or previous year for January)
if (month.month() === 0) { // January
    tR += `[[${prevYear}]]  /  `;
} else {
    tR += `[[${currentYear}]]  /  `;
}

tR += `❮  [[${prevMonth.format("YYYY-MM")}|${prevMonth.format("MMMM")}]]`;
tR += `  |  ${month.format("MMMM")}  |  `;
tR += `[[${nextMonth.format("YYYY-MM")}|${nextMonth.format("MMMM")}]]  ❯`;

// Add next year for December
if (month.month() === 11) { // December
    tR += `  /  [[${nextYear}]]`;
}

tR += "\n\n";

// Weekly Journal - Simplified logic
tR += "## Weekly Journal Entries for this Month\n\n";
const startOfMonth = month.clone().startOf('month');
const endOfMonth = month.clone().endOf('month');
const weeks = new Set();

// Iterate through each day of the month and collect unique weeks
let current = startOfMonth.clone();
while (current.isSameOrBefore(endOfMonth)) {
    const weekFormat = current.format('GGGG-[W]WW'); // Changed to GGGG that is the ISO week-year format
    const weekDisplay = current.format('[Week] w');
    weeks.add(`- [[${weekFormat}|${weekDisplay}]]`);
    current.add(1, 'week').startOf('isoWeek');
}

Array.from(weeks).forEach(week => tR += week + '\n');
%>

## Monthly Journal Sections

…

---
created: <% tp.date.now("YYYY-MM-DD HH:mm") %>
title: <%* 
// Parse filename as ISO week-year format
const weekParsed = moment(tp.file.title, "GGGG-[W]WW");
tR += weekParsed.format("GGGG-[W]WW — [Weekly Note]"); 
%>
last-updated: <% tp.date.now("YYYY-MM-DD HH:mm") %>
---
<%*
// Parse week using ISO week-year format - CRITICAL: use GGGG not YYYY
const week = moment(tp.file.title, "GGGG-[W]WW");
const weekStart = week.clone().startOf('isoWeek');
const weekEnd = week.clone().endOf('isoWeek');

// Validate parsing worked
if (!week.isValid()) {
    tR += "\n# ERROR: Could not parse week from filename\n\n";
    tR += `Filename: ${tp.file.title}\n`;
    return;
}

// Extract calendar years from actual dates (not ISO week-year)
const startCalYear = weekStart.year();
const endCalYear = weekEnd.year();
const isoWeekYear = week.isoWeekYear();

// Header: Week X of YYYY (using ISO week-year)
tR += `\n# ${week.format('[Week] WW [of] GGGG')}\n\n`;

// Build navigation breadcrumb
const startYear = weekStart.format('YYYY');
const startMonth = weekStart.format('YYYY-MM');
const startMonthName = weekStart.format('MMMM');
const endYear = weekEnd.format('YYYY');
const endMonth = weekEnd.format('YYYY-MM');
const endMonthName = weekEnd.format('MMMM');

let breadcrumb = `[[${startYear}]]  /  [[${startMonth}|${startMonthName}]]`;

// If week spans two calendar years
if (startCalYear !== endCalYear) {
    breadcrumb += '  –  [[' + endYear + ']]  /  [[' + endMonth + '|' + endMonthName + ']]';
} else if (weekStart.month() !== weekEnd.month()) {
    // Same year, different months
    breadcrumb += '  –  [[' + endMonth + '|' + endMonthName + ']]';
}

tR += breadcrumb + '\n';

// Week navigation (using ISO week-year)
const prevWeek = week.clone().subtract(1, 'week');
const nextWeek = week.clone().add(1, 'week');
tR += `❮  [[${prevWeek.format('GGGG-[W]WW')}|${prevWeek.format('[Week] WW')}]]  |  ${week.format('[Week] WW')}  |  [[${nextWeek.format('GGGG-[W]WW')}|${nextWeek.format('[Week] WW')}]]  ❯\n`;

// Daily journal section
tR += '\n## Daily Journal Entries for the Week\n\n';

// Generate daily note links
const dailyLinks = Array.from({length: 7}, (_, i) => {
    const date = weekStart.clone().add(i, 'days');
    const fileName = date.format('YYYY-MM-DD');
    const weekday = date.format('dddd');
    return `- [[${fileName}|${fileName} — ${weekday}]]`;
});

tR += dailyLinks.join('\n') + '\n';
%>
## Weekly Journal Sections

…

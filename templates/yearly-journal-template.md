---
created: <% tp.date.now("YYYY-MM-DD HH:mm") %>
title: <%* const titleMoment = moment(tp.file.title, "YYYY"); tR += titleMoment.format("YYYY") + " — Yearly Note"; %>
last-updated: <% tp.date.now("YYYY-MM-DD HH:mm") %>
---
<%*
const yearObject = moment(tp.file.title, "YYYY");
const year = yearObject.format("YYYY");
// const month = moment(tp.file.title, "YYYY-MM");
// const monthPath = month.format('MM-MMMM');
// const monthYear = month.format('MMMM YYYY');

// Header
tR += `\n# ${year}\n\n`;

// Navigation
const prevYearObject = yearObject.clone().subtract(1, "year");
const nextYearObject = yearObject.clone().add(1, "year");
const prevYear = prevYearObject.format("YYYY");
const nextYear = nextYearObject.format("YYYY");

tR += `❮  [[${prevYear}]]`;
tR += `  |  ${year}  |  `;
tR += `[[${nextYear}]]  ❯`;

tR += "\n";

// Monthly Journal - All months in the year
tR += "\n## Monthly Journal Entries for " + year + "\n\n";
for (let monthNum = 0; monthNum <= 11; monthNum++) {
    const monthObject = yearObject.clone().month(monthNum);
    const monthFormat = monthObject.format('YYYY-MM');
    const monthDisplay = monthObject.format('MMMM');
    tR += `- [[${monthFormat}|${monthDisplay}]]\n`;
}

// Weekly Journal - All weeks in the year
tR += "## Weekly Journal Entries for " + year + "\n\n";
const startOfYear = yearObject.clone().startOf('year').startOf('isoWeek');
const endOfYear = yearObject.clone().endOf('year');
const weeks = [];

let current = startOfYear.clone();
while (current.year() <= yearObject.year()) {
    const weekYear = current.format('GGGG');
    if (weekYear === year) {  // Only include weeks that belong to this ISO year
        const weekFormat = current.format('GGGG-[W]WW');
        const weekDisplay = current.format('[Week] W');
        weeks.push(`- [[${weekFormat}|${weekDisplay}]]`);
    }
    current.add(1, 'week');
}

weeks.forEach(week => tR += week + '\n');
%>
## Yearly Journal Sections
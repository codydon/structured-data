<template>
<pre>
    {{ structuredData }}
</pre>
  </template>
  <script setup>




const structuredData = ref('')
  
  // Function to generate the JSON-LD script
  const generateStructuredData = () => {
    structuredData.value = {
      "@context": "https://schema.org",
      "@type": "JobPosting",
      "title": 'job.value.title',
      "description": 'job.value.description',
      "employmentType": 'job.value.employment_type',
      "jobLocation": {
        "@type": "Place",
        "address": {
          "@type": "PostalAddress",
          "addressLocality": 'job.value.job_location',
          "addressCountry": 'job.value.country',
        }
      },
      "datePosted":' job.value.date_posted',
      "validThrough": 'job.value.valid_through',
      "hiringOrganization": {
        "@type": "Organization",
        "name": 'job.value.company.name',
        "sameAs": 'job.value.company.website_uri',
        "logo": 'job.value.company.logo'
      },
      "baseSalary": {
        "@type": "MonetaryAmount",
        "currency": 'job.value.currency',
        "value": {
          "@type": "QuantitativeValue",
          "minValue": 'job.value.min_salary',
          "maxValue": 'job.value.max_salary',
          "unitText": "MONTH"
        }
      },
      // "responsibilities": "..."
    };
  
    useHead({
      script: [{
        type: 'application/ld+json',
        innerHTML: JSON.stringify({
          "type": "application/ld+json",
          "textContent": structuredData.value
        })
      }],
      __dangerouslyDisableSanitizers: ['script'],
    })
    console.log('GENERATED STRUCTURED DATA', structuredData.value)
  }


generateStructuredData();
  
  //layout
  definePageMeta({
    layout: "accounts",
  });
  </script>
    